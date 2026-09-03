# Kata Containers on Raspberry Pi 5 (ARM64)

This repository documents the setup for running **Kata Containers on Raspberry Pi 5 (ARM64)** and building a custom Kata guest kernel with **CUBIC congestion control enabled**.

> **Notation**
>
> - **Command**: command entered manually in the terminal.
> - **Expected output**: representative output used to verify that the step succeeded.
> - Long package installation and kernel compilation logs are omitted.

---

## 1. Install Kata Containers

### 1.1 Download Kata Containers 3.24.0

**Command**

```bash
sudo apt update

wget https://github.com/kata-containers/kata-containers/releases/download/3.24.0/kata-static-3.24.0-arm64.tar.zst
```

Extract the static package:

```bash
sudo tar -xvf kata-static-3.24.0-arm64.tar.zst -C /
rm kata-static-3.24.0-arm64.tar.zst
```

Create command symlinks:

```bash
sudo ln -sfn /opt/kata/bin/kata-runtime \
  /usr/local/bin/kata-runtime

sudo ln -sfn /opt/kata/bin/containerd-shim-kata-v2 \
  /usr/local/bin/containerd-shim-kata-v2

sudo ln -sfn /opt/kata/bin/kata-collect-data.sh \
  /usr/local/bin/kata-collect-data.sh
```

### 1.2 Verify the installation

**Command**

```bash
which kata-runtime
kata-runtime --version
```

**Expected output**

```text
/usr/local/bin/kata-runtime

kata-runtime  : 3.24.0
commit        : c7d0c270ee7dfaa6d978e6e07b99dabdaf2b9fda
OCI specs     : 1.2.1
```

---

## 2. Check Host Kernel Support

Kata Containers requires KVM and vhost-related host kernel modules.

### 2.1 Load vhost modules

**Command**

```bash
sudo modprobe vhost
sudo modprobe vhost_net
sudo modprobe vhost_vsock
```

### 2.2 Verify loaded modules

**Command**

```bash
lsmod | grep -E 'vhost|vsock|tap'
```

**Example output**

```text
vhost_vsock
vmw_vsock_virtio_transport_common
vsock
vhost_net
tap
vhost
vhost_iotlb
```

The module sizes and reference counts can differ depending on the host kernel.

### 2.3 Check Kata compatibility

**Command**

```bash
sudo kata-runtime check
```

**Expected output**

```text
System is capable of running Kata Containers
System can currently create Kata Containers
```

---

# 3. Install Guest Kernel Build Dependencies

### 3.1 Install required packages

**Command**

```bash
sudo apt update

sudo apt install -y \
  flex \
  bison \
  libelf-dev \
  libncurses-dev \
  curl \
  git
```

---

# 4. Install Go and Rust

## 4.1 Install Go

Download Go:

```bash
wget https://go.dev/dl/go1.26.0.linux-arm64.tar.gz
```

Remove any existing manual Go installation:

```bash
sudo rm -rf /usr/local/go
```

Install Go:

```bash
sudo tar -C /usr/local \
  -xzf go1.26.0.linux-arm64.tar.gz
```

Remove the archive:

```bash
rm -f go1.26.0.linux-arm64.tar.gz
```

Add Go to the **front** of `PATH`:

```bash
sed -i '\|export PATH=$PATH:/usr/local/go/bin|d' ~/.bashrc

echo 'export PATH=/usr/local/go/bin:$PATH' >> ~/.bashrc

source ~/.bashrc
hash -r
```

> `/usr/local/go/bin` must come before `/usr/bin` so that an older Ubuntu Go installation is not selected first.

Verify:

```bash
which go
go version
```

**Expected output**

```text
/usr/local/go/bin/go
go version go1.26.0 linux/arm64
```

---

## 4.2 Install Rust

**Command**

```bash
curl https://sh.rustup.rs -sSf | sh -s -- -y
```

Load the Rust environment:

```bash
source "$HOME/.cargo/env"
```

Verify:

```bash
rustc --version
cargo --version
```

**Example output**

```text
rustc 1.98.0 (...)
cargo 1.98.0 (...)
```

---

# 5. Install yq and Clone Kata Containers

## 5.1 Install yq

**Command**

```bash
go install github.com/mikefarah/yq/v4@v4.52.4
```

Add the Go user binary directory to `PATH`:

```bash
echo 'export PATH=$HOME/go/bin:$PATH' >> ~/.bashrc
source ~/.bashrc
```

Copy `yq` to `/usr/local/bin`:

```bash
sudo cp "$HOME/go/bin/yq" /usr/local/bin/yq
```

Verify:

```bash
yq --version
```

**Expected output**

```text
yq (...) version v4.52.4
```

---

## 5.2 Clone Kata Containers

This guide uses the current Kata Containers repository for the guest-kernel build.

**Command**

```bash
git clone \
  https://github.com/kata-containers/kata-containers.git \
  ~/kata-containers
```

If the repository already exists:

```bash
cd ~/kata-containers
git pull
```

---

# 6. Prepare the Kata Guest Kernel

This setup uses Linux **6.12.47** as the guest-kernel base.

Move to the kernel packaging directory:

```bash
cd ~/kata-containers/tools/packaging/kernel
```

Run the setup step:

```bash
./build-kernel.sh \
  -a aarch64 \
  -v 6.12.47 \
  -f \
  -d \
  setup
```

**Expected result**

A successful setup should end with output similar to:

```text
INFO: Kernel version: 6.12.47
Kernel source ready: .../kata-linux-6.12.47-<CONFIG_VERSION>
```

The Kata config revision depends on the repository revision.

---

# 7. Enable CUBIC in the Kata Guest Kernel

The default Kata configuration used in this setup enables BBR but does not enable CUBIC.

We enable:

```text
CUBIC = built-in
BBR   = built-in
Default CCA = CUBIC
```

This also allows CUBIC and BBR to be switched later without rebuilding the kernel.

---

## 7.1 Determine the kernel directory

**Command**

```bash
cd ~/kata-containers/tools/packaging/kernel

CFG=$(cat kata_config_version)
KDIR="$PWD/kata-linux-6.12.47-$CFG"

echo "CFG=$CFG"
echo "KDIR=$KDIR"
```

**Example output**

```text
CFG=202
KDIR=/home/rpi3/kata-containers/tools/packaging/kernel/kata-linux-6.12.47-202
```

> `202` is only an example.  
> Always use the value returned by `kata_config_version`.

---

## 7.2 Enable CUBIC

**Command**

```bash
"$KDIR/scripts/config" \
  --file "$KDIR/.config" \
  -e TCP_CONG_CUBIC \
  -e TCP_CONG_BBR \
  -e DEFAULT_CUBIC \
  -d DEFAULT_BBR
```

Resolve Kconfig dependencies:

```bash
make -C "$KDIR" ARCH=arm64 olddefconfig
```

---

## 7.3 Verify the CCA kernel configuration

**Command**

```bash
grep -E \
'CONFIG_TCP_CONG_(CUBIC|BBR)|CONFIG_DEFAULT_(CUBIC|BBR)|CONFIG_DEFAULT_TCP_CONG' \
"$KDIR/.config"
```

**Expected output**

```text
CONFIG_TCP_CONG_CUBIC=y
CONFIG_TCP_CONG_BBR=y
CONFIG_DEFAULT_CUBIC=y
# CONFIG_DEFAULT_BBR is not set
CONFIG_DEFAULT_TCP_CONG="cubic"
```

If this output is correct, CUBIC is compiled directly into the guest kernel.

> Do **not** execute `setup -f` again after modifying `.config`, because the setup process can regenerate the configuration.

---

# 8. Build the Kata Guest Kernel

## 8.1 Build

**Command**

```bash
cd ~/kata-containers/tools/packaging/kernel

./build-kernel.sh \
  -a aarch64 \
  -v 6.12.47 \
  -d \
  build
```

The kernel build can take several minutes.

Long `CC`, `AR`, and `LD` build messages are normal.

---

## 8.2 Verify generated kernel files

**Command**

```bash
ls -lh "$KDIR/vmlinux"

ls -lh "$KDIR/arch/arm64/boot/Image"

ls -lh "$KDIR/arch/arm64/boot/Image.gz"
```

**Expected result**

The following files should exist:

```text
vmlinux
arch/arm64/boot/Image
arch/arm64/boot/Image.gz
```

---

# 9. Install the Guest Kernel

`build-kernel.sh install` requires root privileges.

**Command**

```bash
sudo ./build-kernel.sh \
  -a aarch64 \
  -v 6.12.47 \
  -d \
  install
```

The kernel is installed under:

```text
/usr/share/kata-containers/
```

Verify:

```bash
ls -lh /usr/share/kata-containers/
```

**Expected files**

```text
vmlinuz-6.12.47-<CONFIG_VERSION>
vmlinux-6.12.47-<CONFIG_VERSION>
config-6.12.47-<CONFIG_VERSION>

vmlinuz.container
vmlinux.container
```

---

# 10. Copy the Custom Kernel to the Static Kata Installation

The Kata 3.24.0 static package is installed under:

```text
/opt/kata/
```

However, the kernel build script installs the custom kernel under:

```text
/usr/share/kata-containers/
```

Therefore, copy the new kernel into the `/opt/kata` installation.

---

## 10.1 Check the current Kata kernel

**Command**

```bash
readlink -f \
  /opt/kata/share/kata-containers/vmlinuz.container

readlink -f \
  /opt/kata/share/kata-containers/vmlinux.container
```

Also check Kata runtime information:

```bash
sudo kata-runtime env | grep -i -A5 kernel
```

---

## 10.2 Back up the current kernel symlinks

**Command**

```bash
sudo cp -a \
  /opt/kata/share/kata-containers/vmlinuz.container \
  /opt/kata/share/kata-containers/vmlinuz.container.backup
```

```bash
sudo cp -a \
  /opt/kata/share/kata-containers/vmlinux.container \
  /opt/kata/share/kata-containers/vmlinux.container.backup
```

---

## 10.3 Copy the custom kernel

**Command**

```bash
sudo cp \
  "/usr/share/kata-containers/vmlinuz-6.12.47-$CFG" \
  "/opt/kata/share/kata-containers/vmlinuz-6.12.47-$CFG"
```

```bash
sudo cp \
  "/usr/share/kata-containers/vmlinux-6.12.47-$CFG" \
  "/opt/kata/share/kata-containers/vmlinux-6.12.47-$CFG"
```

```bash
sudo cp \
  "/usr/share/kata-containers/config-6.12.47-$CFG" \
  "/opt/kata/share/kata-containers/config-6.12.47-$CFG"
```

---

## 10.4 Point Kata kernel symlinks to the custom kernel

**Command**

```bash
cd /opt/kata/share/kata-containers
```

```bash
sudo ln -sfn \
  "vmlinuz-6.12.47-$CFG" \
  vmlinuz.container
```

```bash
sudo ln -sfn \
  "vmlinux-6.12.47-$CFG" \
  vmlinux.container
```

Verify:

```bash
readlink -f vmlinuz.container
readlink -f vmlinux.container
```

> An already-running Kata microVM continues using the old guest kernel.  
> Stop and recreate the Kata container after changing the kernel.

---

# 11. Check CNI Plugins

## 11.1 Check CNI binaries

**Command**

```bash
ls /opt/cni/bin/
```

**Example output**

```text
bandwidth
bridge
dhcp
firewall
host-device
host-local
ipvlan
loopback
macvlan
portmap
ptp
tuning
vlan
vrf
```

---

## 11.2 Check the bridge plugin

**Command**

```bash
/opt/cni/bin/bridge 2>&1 | head -3
```

**Example output**

```text
CNI bridge plugin v1.2.0
CNI protocol versions supported: ...
```

---

## 11.3 Check the CNI package

**Command**

```bash
dpkg -l | grep -i cni
```

**Example output**

```text
ii  kubernetes-cni  1.2.0-2.1  ...
```

---

## 11.4 Check containerd CNI configuration

**Command**

```bash
containerd config dump | grep -i cni
```

The configuration should point to:

```text
bin_dir = "/opt/cni/bin"
conf_dir = "/etc/cni/net.d"
```

You can also check:

```bash
crictl info 2>/dev/null | grep -i cni
```

---

# 12. Configure Kata Runtime in containerd

## 12.1 Back up the containerd configuration

**Command**

```bash
sudo cp \
  /etc/containerd/config.toml \
  /etc/containerd/config.toml.bak
```

Open the configuration file:

```bash
sudo nano /etc/containerd/config.toml
```

---

## 12.2 Add the Kata runtime

If the file contains a runtime section such as:

```toml
[plugins."io.containerd.cri.v1.runtime".containerd.runtimes.runc]
```

add the following block:

```toml
[plugins."io.containerd.cri.v1.runtime".containerd.runtimes.kata]
  runtime_type = "io.containerd.kata.v2"
```

Do **not** remove the existing `runc` runtime.

For example:

```toml
[plugins."io.containerd.cri.v1.runtime".containerd.runtimes.runc]
  runtime_type = "io.containerd.runc.v2"

[plugins."io.containerd.cri.v1.runtime".containerd.runtimes.runc.options]
  SystemdCgroup = true

[plugins."io.containerd.cri.v1.runtime".containerd.runtimes.kata]
  runtime_type = "io.containerd.kata.v2"
```

> Older containerd versions can use:
>
> ```toml
> [plugins."io.containerd.grpc.v1.cri".containerd.runtimes.kata]
> ```
>
> Use the same plugin namespace already used by the existing `runc` section in your `config.toml`.

---

## 12.3 Restart containerd

**Command**

```bash
sudo systemctl restart containerd
```

Check status:

```bash
sudo systemctl status containerd --no-pager
```

Verify Kata runtime configuration:

```bash
sudo containerd config dump | grep -A5 -B2 kata
```

---

# 13. Configure the CNI Network

Create the CNI configuration directory:

```bash
sudo mkdir -p /etc/cni/net.d
```

Create:

```text
/etc/cni/net.d/10-mynet.conf
```

**Command**

```bash
sudo tee /etc/cni/net.d/10-mynet.conf > /dev/null <<'EOF'
{
  "cniVersion": "0.2.0",
  "name": "mynet",
  "type": "bridge",
  "bridge": "cni0",
  "isGateway": true,
  "ipMasq": true,
  "ipam": {
    "type": "host-local",
    "subnet": "172.19.0.0/24",
    "routes": [
      {
        "dst": "0.0.0.0/0"
      }
    ]
  },
  "dns": {
    "nameservers": [
      "155.230.10.2"
    ]
  }
}
EOF
```

Verify:

```bash
cat /etc/cni/net.d/10-mynet.conf
```

> `155.230.10.2` is the DNS server used in this environment.  
> Replace it if another DNS server is required.

Restart containerd:

```bash
sudo systemctl restart containerd
```

---

# 14. Install nerdctl

## 14.1 Download nerdctl 2.2.1

**Command**

```bash
wget \
  https://github.com/containerd/nerdctl/releases/download/v2.2.1/nerdctl-2.2.1-linux-arm64.tar.gz
```

Extract:

```bash
tar xzvf nerdctl-2.2.1-linux-arm64.tar.gz
```

Install:

```bash
sudo cp nerdctl /usr/local/bin/nerdctl
```

Clean up:

```bash
rm -f nerdctl-2.2.1-linux-arm64.tar.gz
```

Verify:

```bash
nerdctl --version
```

**Expected output**

```text
nerdctl version 2.2.1
```

---

# 15. Run a Kata Container

Run Ubuntu using the Kata runtime:

```bash
sudo nerdctl run \
  -it \
  --rm \
  --runtime io.containerd.kata.v2 \
  ubuntu:latest \
  /bin/bash
```

You should now enter the Ubuntu container running inside the Kata microVM.

Example prompt:

```text
root@<container-id>:/#
```

---

# 16. Verify the Kata Guest Kernel

Run the following commands **inside the Kata container**.

## 16.1 Check the guest kernel

**Command**

```bash
uname -a
```

---

## 16.2 Check the current congestion-control algorithm

**Command**

```bash
sysctl net.ipv4.tcp_congestion_control
```

**Expected output**

```text
net.ipv4.tcp_congestion_control = cubic
```

---

## 16.3 Check available CCAs

**Command**

```bash
cat /proc/sys/net/ipv4/tcp_available_congestion_control
```

**Expected result**

The output should contain:

```text
reno cubic bbr
```

The order can differ.

The important point is that both:

```text
cubic
bbr
```

are available.

---

# 17. Switch Between CUBIC and BBR

Because both algorithms are built into the same guest kernel, the CCA can be changed without rebuilding the kernel.

## Use CUBIC

```bash
sysctl -w net.ipv4.tcp_congestion_control=cubic
```

Verify:

```bash
sysctl net.ipv4.tcp_congestion_control
```

**Expected output**

```text
net.ipv4.tcp_congestion_control = cubic
```

---

## Use BBR

```bash
sysctl -w net.ipv4.tcp_congestion_control=bbr
```

Verify:

```bash
sysctl net.ipv4.tcp_congestion_control
```

**Expected output**

```text
net.ipv4.tcp_congestion_control = bbr
```

This allows CUBIC and BBR experiments to use the **same Kata guest kernel**.

---

# 18. Troubleshooting

## 18.1 `build-kernel.sh install` returns `Permission denied`

Example:

```text
install: cannot create directory '/usr/share/kata-containers': Permission denied
```

Run the install step using `sudo`:

```bash
sudo ./build-kernel.sh \
  -a aarch64 \
  -v 6.12.47 \
  -d \
  install
```

---

## 18.2 CUBIC does not appear inside the Kata guest

Check the host-side guest-kernel config:

```bash
grep -E \
'CONFIG_TCP_CONG_(CUBIC|BBR)|CONFIG_DEFAULT_(CUBIC|BBR)|CONFIG_DEFAULT_TCP_CONG' \
"$KDIR/.config"
```

The important setting is:

```text
CONFIG_TCP_CONG_CUBIC=y
```

The complete expected configuration is:

```text
CONFIG_TCP_CONG_CUBIC=y
CONFIG_TCP_CONG_BBR=y
CONFIG_DEFAULT_CUBIC=y
# CONFIG_DEFAULT_BBR is not set
CONFIG_DEFAULT_TCP_CONG="cubic"
```

If the config is correct but the guest still reports:

```text
reno bbr
```

check which kernel Kata is using:

```bash
readlink -f \
  /opt/kata/share/kata-containers/vmlinuz.container
```

```bash
readlink -f \
  /opt/kata/share/kata-containers/vmlinux.container
```

Then stop the existing Kata microVM and create a new container.

---

## 18.3 Bash shows a `>` prompt

If a command ends with:

```bash
\
```

Bash expects another line.

For example:

```bash
cat /proc/sys/net/ipv4/tcp_available_congestion_control\
```

causes:

```text
>
```

Use:

```bash
cat /proc/sys/net/ipv4/tcp_available_congestion_control
```

Press:

```text
Ctrl+C
```

to cancel an accidental continuation prompt.

---

# Final Verification

On the **host**, the custom guest-kernel configuration should contain:

```text
CONFIG_TCP_CONG_CUBIC=y
CONFIG_TCP_CONG_BBR=y
CONFIG_DEFAULT_CUBIC=y
# CONFIG_DEFAULT_BBR is not set
CONFIG_DEFAULT_TCP_CONG="cubic"
```

Inside a **newly created Kata container**:

```bash
sysctl net.ipv4.tcp_congestion_control
```

should return:

```text
net.ipv4.tcp_congestion_control = cubic
```

and:

```bash
cat /proc/sys/net/ipv4/tcp_available_congestion_control
```

should contain:

```text
reno cubic bbr
```

At this point, the Kata guest supports both **CUBIC** and **BBR**, with **CUBIC configured as the default congestion-control algorithm**.
