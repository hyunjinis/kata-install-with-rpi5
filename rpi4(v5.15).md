# Kata Containers on Raspberry Pi 4 (ARM64)

This repository documents the setup for running **Kata Containers on Raspberry Pi 4 (ARM64)** and building a custom Kata guest kernel with **CUBIC congestion control enabled**.

The tested configuration is:

```text
Board                 Raspberry Pi 4
Architecture          ARM64
Host OS               Ubuntu 22.04
Host kernel           5.15.0-1105-raspi

Kata Containers       3.24.0
Kata guest kernel     Linux 6.12.47
nerdctl               2.2.1

Guest CCA             CUBIC (default)
Available guest CCAs  CUBIC + BBR
```

> **Important**
>
> The Kata **guest kernel** does not need to match the host kernel.
>
> In this setup:
>
> ```text
> RPi4 host kernel     = 5.15.x
> Kata guest kernel    = 6.12.47
> ```
>
> This is intentional.

> **Notation**
>
> - **Command**: command entered manually in the terminal.
> - **Expected output**: representative output used to verify that the step succeeded.
> - Long package installation and kernel compilation logs are omitted.

---

# 1. Install Kata Containers

## 1.1 Download Kata Containers 3.24.0

**Command**

```bash
sudo apt update

wget \
  https://github.com/kata-containers/kata-containers/releases/download/3.24.0/kata-static-3.24.0-arm64.tar.zst
```

Extract the static package:

```bash
sudo tar -xvf \
  kata-static-3.24.0-arm64.tar.zst \
  -C /

rm -f kata-static-3.24.0-arm64.tar.zst
```

Create command symlinks:

```bash
sudo ln -sfn \
  /opt/kata/bin/kata-runtime \
  /usr/local/bin/kata-runtime

sudo ln -sfn \
  /opt/kata/bin/containerd-shim-kata-v2 \
  /usr/local/bin/containerd-shim-kata-v2

sudo ln -sfn \
  /opt/kata/bin/kata-collect-data.sh \
  /usr/local/bin/kata-collect-data.sh
```

---

## 1.2 Verify the installation

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

# 2. Prepare Raspberry Pi 4 Host Kernel Support

Kata Containers requires KVM, vhost, TAP, traffic-control, and network-namespace support.

On the Raspberry Pi 4 Ubuntu 5.15 kernel used in this setup, an additional requirement is particularly important:

```text
xfrm_user
```

Without `xfrm_user`, `NETLINK_XFRM` can be unavailable and Kata networking can fail with:

```text
failed to create shim task: protocol not supported
```

---

## 2.1 Check the host kernel

**Command**

```bash
uname -r
```

**Tested output**

```text
5.15.0-1105-raspi
```

---

## 2.2 Install additional kernel modules

Install the modules package corresponding to the **currently running kernel**:

```bash
sudo apt update

sudo apt install -y \
  linux-modules-extra-$(uname -r)
```

This step is important because `xfrm_user` may not be present in a minimal Raspberry Pi kernel installation.

---

## 2.3 Load required Kata networking modules

**Command**

```bash
sudo modprobe xfrm_user

sudo modprobe vhost
sudo modprobe vhost_net
sudo modprobe vhost_vsock

sudo modprobe sch_ingress
sudo modprobe cls_u32
sudo modprobe act_mirred
```

`vhost_net` normally loads the required TAP support automatically.

---

## 2.4 Verify loaded modules

**Command**

```bash
lsmod | grep -E \
'xfrm_user|xfrm_algo|vhost|tap|sch_ingress|cls_u32|act_mirred'
```

**Representative output**

```text
xfrm_user
xfrm_algo

act_mirred
cls_u32
sch_ingress

vhost_net
tap
vhost_vsock
vhost
vhost_iotlb
```

Module sizes and reference counts can differ.

---

## 2.5 Automatically load the modules after reboot

Create:

```text
/etc/modules-load.d/kata-rpi4.conf
```

**Command**

```bash
sudo tee \
  /etc/modules-load.d/kata-rpi4.conf \
  > /dev/null <<'EOF'
xfrm_user
vhost
vhost_net
vhost_vsock
sch_ingress
cls_u32
act_mirred
EOF
```

Verify:

```bash
cat /etc/modules-load.d/kata-rpi4.conf
```

---

## 2.6 Verify TUN and vhost devices

**Command**

```bash
ls -l /dev/net/tun
ls -l /dev/vhost-net
ls -l /dev/vhost-vsock
```

The device nodes should exist.

---

## 2.7 Verify required Netlink protocols

Kata accesses networking information through Netlink.

Check the three relevant Netlink families:

```bash
python3 - <<'PY'
import socket

for proto, name in [
    (0,  "NETLINK_ROUTE"),
    (6,  "NETLINK_XFRM"),
    (12, "NETLINK_NETFILTER"),
]:
    try:
        s = socket.socket(
            socket.AF_NETLINK,
            socket.SOCK_RAW,
            proto
        )
        print(f"{name}: OK")
        s.close()
    except OSError as e:
        print(
            f"{name}: FAIL "
            f"errno={e.errno} {e}"
        )
PY
```

**Expected output**

```text
NETLINK_ROUTE: OK
NETLINK_XFRM: OK
NETLINK_NETFILTER: OK
```

If:

```text
NETLINK_XFRM: FAIL errno=93 Protocol not supported
```

appears, load:

```bash
sudo modprobe xfrm_user
```

and repeat the test.

---

## 2.8 Check Kata host compatibility

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
wget \
  https://go.dev/dl/go1.26.0.linux-arm64.tar.gz
```

Remove an existing manually installed Go:

```bash
sudo rm -rf /usr/local/go
```

Install:

```bash
sudo tar \
  -C /usr/local \
  -xzf go1.26.0.linux-arm64.tar.gz
```

Remove the archive:

```bash
rm -f go1.26.0.linux-arm64.tar.gz
```

Put `/usr/local/go/bin` at the front of `PATH`:

```bash
sed -i \
  '\|export PATH=$PATH:/usr/local/go/bin|d' \
  ~/.bashrc

echo \
  'export PATH=/usr/local/go/bin:$PATH' \
  >> ~/.bashrc

source ~/.bashrc
hash -r
```

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
curl \
  https://sh.rustup.rs \
  -sSf | sh -s -- -y
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

---

# 5. Install yq and Clone Kata Containers

## 5.1 Install yq

**Command**

```bash
go install \
  github.com/mikefarah/yq/v4@v4.52.4
```

Add the Go user binary directory to `PATH`:

```bash
echo \
  'export PATH=$HOME/go/bin:$PATH' \
  >> ~/.bashrc

source ~/.bashrc
```

Install `yq` globally:

```bash
sudo cp \
  "$HOME/go/bin/yq" \
  /usr/local/bin/yq
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

This setup uses Linux:

```text
6.12.47
```

as the Kata guest-kernel base.

Move to:

```bash
cd \
  ~/kata-containers/tools/packaging/kernel
```

Run the kernel setup:

```bash
./build-kernel.sh \
  -a aarch64 \
  -v 6.12.47 \
  -f \
  -d \
  setup
```

**Expected result**

```text
INFO: Kernel version: 6.12.47
Kernel source ready: .../kata-linux-6.12.47-<CONFIG_VERSION>
```

The Kata configuration revision depends on the repository revision.

---

# 7. Enable CUBIC in the Kata Guest Kernel

The guest kernel is configured so that:

```text
CUBIC = built-in
BBR   = built-in

Default TCP CCA = CUBIC
```

This allows CUBIC and BBR to be switched at runtime without rebuilding the guest kernel.

---

## 7.1 Determine the Kata kernel configuration revision

**Command**

```bash
cd \
  ~/kata-containers/tools/packaging/kernel

CFG=$(cat kata_config_version)

KDIR="$PWD/kata-linux-6.12.47-$CFG"

echo "CFG=$CFG"
echo "KDIR=$KDIR"
```

**Example**

```text
CFG=202

KDIR=/home/ubuntu2/kata-containers/tools/packaging/kernel/kata-linux-6.12.47-202
```

The value `202` is only an example.

Always use the value returned by:

```bash
cat kata_config_version
```

---

## 7.2 Enable CUBIC and BBR

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
make \
  -C "$KDIR" \
  ARCH=arm64 \
  olddefconfig
```

---

## 7.3 Verify the guest CCA configuration

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

> Do not run the force setup step again after modifying `.config`.
>
> Running:
>
> ```bash
> ./build-kernel.sh ... -f ... setup
> ```
>
> again can regenerate the kernel configuration.

---

# 8. Build the Kata Guest Kernel

## 8.1 Build

**Command**

```bash
cd \
  ~/kata-containers/tools/packaging/kernel

./build-kernel.sh \
  -a aarch64 \
  -v 6.12.47 \
  -d \
  build
```

The build can take several minutes.

---

## 8.2 Verify generated files

**Command**

```bash
ls -lh "$KDIR/vmlinux"

ls -lh \
  "$KDIR/arch/arm64/boot/Image"

ls -lh \
  "$KDIR/arch/arm64/boot/Image.gz"
```

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
cd \
  ~/kata-containers/tools/packaging/kernel

sudo ./build-kernel.sh \
  -a aarch64 \
  -v 6.12.47 \
  -d \
  install
```

The generated files are installed under:

```text
/usr/share/kata-containers/
```

Verify:

```bash
ls -lh \
  /usr/share/kata-containers/
```

Expected files include:

```text
vmlinuz-6.12.47-<CONFIG_VERSION>
vmlinux-6.12.47-<CONFIG_VERSION>
config-6.12.47-<CONFIG_VERSION>

vmlinuz.container
vmlinux.container
```

---

# 10. Install the Custom Guest Kernel into Static Kata

The Kata 3.24.0 static package uses:

```text
/opt/kata/
```

while the kernel build script installs into:

```text
/usr/share/kata-containers/
```

The custom kernel therefore needs to be copied into the static installation.

---

## 10.1 Check the current guest kernel

```bash
readlink -f \
  /opt/kata/share/kata-containers/vmlinuz.container

readlink -f \
  /opt/kata/share/kata-containers/vmlinux.container
```

Also check:

```bash
sudo kata-runtime env \
  | grep -i -A5 kernel
```

---

## 10.2 Back up the current symlinks

```bash
sudo cp -a \
  /opt/kata/share/kata-containers/vmlinuz.container \
  /opt/kata/share/kata-containers/vmlinuz.container.backup

sudo cp -a \
  /opt/kata/share/kata-containers/vmlinux.container \
  /opt/kata/share/kata-containers/vmlinux.container.backup
```

---

## 10.3 Copy the custom kernel

```bash
sudo cp \
  "/usr/share/kata-containers/vmlinuz-6.12.47-$CFG" \
  "/opt/kata/share/kata-containers/vmlinuz-6.12.47-$CFG"

sudo cp \
  "/usr/share/kata-containers/vmlinux-6.12.47-$CFG" \
  "/opt/kata/share/kata-containers/vmlinux-6.12.47-$CFG"

sudo cp \
  "/usr/share/kata-containers/config-6.12.47-$CFG" \
  "/opt/kata/share/kata-containers/config-6.12.47-$CFG"
```

---

## 10.4 Point Kata to the custom guest kernel

```bash
cd \
  /opt/kata/share/kata-containers
```

```bash
sudo ln -sfn \
  "vmlinuz-6.12.47-$CFG" \
  vmlinuz.container

sudo ln -sfn \
  "vmlinux-6.12.47-$CFG" \
  vmlinux.container
```

Verify:

```bash
readlink -f vmlinuz.container
readlink -f vmlinux.container
```

A running Kata VM continues to use the old kernel.

Stop the old VM and create a new Kata container after changing the kernel.

---

# 11. Configure the Kata Runtime

Create a local Kata configuration file so that the runtime configuration used by the experiment is explicit.

```bash
sudo mkdir -p \
  /etc/kata-containers
```

If the configuration file does not already exist:

```bash
sudo cp \
  /opt/kata/share/defaults/kata-containers/configuration-qemu.toml \
  /etc/kata-containers/configuration.toml
```

Verify:

```bash
sudo kata-runtime env \
  > /tmp/kata-env.txt 2>&1

grep -nE \
'Runtime|Config|Path' \
/tmp/kata-env.txt
```

The runtime configuration should point to:

```text
/etc/kata-containers/configuration.toml
```

---

## 11.1 Verify the networking model

**Command**

```bash
grep -nE \
'^[[:space:]]*(internetworking_model|disable_new_netns)[[:space:]]*=' \
/etc/kata-containers/configuration.toml
```

The configuration used for normal Kata networking should be:

```text
internetworking_model = "tcfilter"
disable_new_netns = false
```

If necessary:

```bash
sudo sed -i -E \
's/^[[:space:]]*#?[[:space:]]*internetworking_model[[:space:]]*=.*/internetworking_model = "tcfilter"/' \
/etc/kata-containers/configuration.toml

sudo sed -i -E \
's/^[[:space:]]*#?[[:space:]]*disable_new_netns[[:space:]]*=.*/disable_new_netns = false/' \
/etc/kata-containers/configuration.toml
```

---

# 12. Install and Check CNI Plugins

## 12.1 Install CNI plugins

```bash
sudo apt update

sudo apt install -y \
  kubernetes-cni
```

---

## 12.2 Verify CNI binaries

```bash
ls /opt/cni/bin/
```

The directory should contain plugins such as:

```text
bridge
firewall
host-local
loopback
portmap
ptp
tuning
```

Verify the bridge plugin:

```bash
/opt/cni/bin/bridge \
  2>&1 | head -3
```

---

# 13. Configure Kata Runtime in containerd

Back up the current configuration:

```bash
sudo cp \
  /etc/containerd/config.toml \
  /etc/containerd/config.toml.bak
```

Open:

```bash
sudo nano \
  /etc/containerd/config.toml
```

Find the existing `runc` runtime section.

For containerd 2.x it can look like:

```toml
[plugins."io.containerd.cri.v1.runtime".containerd.runtimes.runc]
  runtime_type = "io.containerd.runc.v2"

  [plugins."io.containerd.cri.v1.runtime".containerd.runtimes.runc.options]
    SystemdCgroup = true
```

Add:

```toml
[plugins."io.containerd.cri.v1.runtime".containerd.runtimes.kata]
  runtime_type = "io.containerd.kata.v2"
```

Do not remove the existing `runc` runtime.

> Use the same plugin namespace already used by the existing `runc` configuration.

Restart containerd:

```bash
sudo systemctl restart containerd
```

Verify:

```bash
sudo systemctl status \
  containerd \
  --no-pager
```

Check the runtime configuration:

```bash
sudo containerd config dump \
  | grep -A5 -B2 kata
```

---

# 14. Install nerdctl

This setup uses:

```text
nerdctl 2.2.1
```

Download:

```bash
wget \
  https://github.com/containerd/nerdctl/releases/download/v2.2.1/nerdctl-2.2.1-linux-arm64.tar.gz
```

Extract:

```bash
tar xzvf \
  nerdctl-2.2.1-linux-arm64.tar.gz
```

Install:

```bash
sudo cp \
  nerdctl \
  /usr/local/bin/nerdctl
```

Clean up:

```bash
rm -f \
  nerdctl-2.2.1-linux-arm64.tar.gz
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

# 15. Create the Kata Test Network

Instead of relying on an implicit default network, create an explicit nerdctl network.

**Command**

```bash
sudo nerdctl network create \
  kata-net
```

Verify:

```bash
sudo nerdctl network ls
```

Inspect:

```bash
sudo nerdctl network inspect \
  kata-net
```

A subnet and gateway should be assigned automatically.

For example:

```text
Subnet   10.4.x.0/24
Gateway  10.4.x.1
```

---

# 16. Verify the Network with a Normal Container

Before running Kata, verify the same CNI network using the normal OCI runtime.

```bash
sudo nerdctl run \
  --rm \
  --network kata-net \
  busybox \
  sh -c \
  'ip addr; echo "=== ROUTE ==="; ip route; echo "=== PING ==="; ping -c 2 1.1.1.1'
```

Expected:

```text
eth0
IPv4 address assigned
default route present
ping succeeds
```

---

# 17. Run a Kata Container

Run Ubuntu 22.04 using the Kata runtime and the same network.

```bash
sudo nerdctl run \
  -it \
  --rm \
  --network kata-net \
  --runtime io.containerd.kata.v2 \
  ubuntu:22.04 \
  sh
```

The following warning can appear:

```text
WARN[0000] cannot set cgroup manager to "systemd" for runtime "io.containerd.kata.v2"
```

This warning is non-fatal if the Kata guest starts normally.

Successful startup should enter a shell:

```text
#
```

---

# 18. Verify the Kata Guest

Run the following commands **inside the Kata container**.

---

## 18.1 Check the guest kernel

```bash
uname -r
```

**Expected**

```text
6.12.47
```

The Kata configuration revision such as `202` does not necessarily appear in `uname -r`.

---

## 18.2 Check the current CCA

```bash
sysctl \
  net.ipv4.tcp_congestion_control
```

**Expected output**

```text
net.ipv4.tcp_congestion_control = cubic
```

---

## 18.3 Check available CCAs

```bash
cat \
  /proc/sys/net/ipv4/tcp_available_congestion_control
```

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

## 18.4 Verify guest networking

Ubuntu does not include `ip` and `ping` in the minimal image by default.

Install:

```bash
apt update

apt install -y \
  iproute2 \
  iputils-ping
```

Check the interface:

```bash
ip addr
```

Check routing:

```bash
ip route
```

Check external connectivity:

```bash
ping -c 3 \
  1.1.1.1
```

Expected:

```text
eth0 present
IPv4 address assigned
default route present
0% packet loss
```

---

# 19. Switch Between CUBIC and BBR

Both congestion-control algorithms are built into the same guest kernel.

Therefore, CUBIC and BBR can be compared without changing the guest-kernel binary.

---

## 19.1 Use CUBIC

```bash
sysctl -w \
  net.ipv4.tcp_congestion_control=cubic
```

Verify:

```bash
sysctl \
  net.ipv4.tcp_congestion_control
```

Expected:

```text
net.ipv4.tcp_congestion_control = cubic
```

---

## 19.2 Use BBR

```bash
sysctl -w \
  net.ipv4.tcp_congestion_control=bbr
```

Verify:

```bash
sysctl \
  net.ipv4.tcp_congestion_control
```

Expected:

```text
net.ipv4.tcp_congestion_control = bbr
```

This allows CUBIC and BBR experiments to use the **same Kata guest kernel**.

---

# 20. Verify Module Persistence After Reboot

Before collecting experimental results, reboot the Raspberry Pi once and verify that the required host modules load automatically.

```bash
sudo reboot
```

After reconnecting:

```bash
uname -r
```

Then:

```bash
lsmod | grep -E \
'xfrm_user|xfrm_algo|vhost|tap|sch_ingress|cls_u32|act_mirred'
```

Verify Netlink support again:

```bash
python3 - <<'PY'
import socket

for proto, name in [
    (0,  "NETLINK_ROUTE"),
    (6,  "NETLINK_XFRM"),
    (12, "NETLINK_NETFILTER"),
]:
    try:
        s = socket.socket(
            socket.AF_NETLINK,
            socket.SOCK_RAW,
            proto
        )
        print(f"{name}: OK")
        s.close()
    except OSError as e:
        print(
            f"{name}: FAIL "
            f"errno={e.errno} {e}"
        )
PY
```

Expected:

```text
NETLINK_ROUTE: OK
NETLINK_XFRM: OK
NETLINK_NETFILTER: OK
```

Finally:

```bash
sudo nerdctl run \
  -it \
  --rm \
  --network kata-net \
  --runtime io.containerd.kata.v2 \
  ubuntu:22.04 \
  sh
```

Inside the guest:

```bash
uname -r

sysctl \
  net.ipv4.tcp_congestion_control

cat \
  /proc/sys/net/ipv4/tcp_available_congestion_control
```

Expected:

```text
6.12.47

net.ipv4.tcp_congestion_control = cubic

reno cubic bbr
```

---

# 21. Troubleshooting

## 21.1 `protocol not supported` when Kata networking is enabled

Example:

```text
failed to create shim task: protocol not supported
```

First check `xfrm_user`:

```bash
lsmod | grep xfrm
```

If `xfrm_user` is missing:

```bash
sudo modprobe xfrm_user
```

If the module itself is unavailable:

```bash
sudo apt install -y \
  linux-modules-extra-$(uname -r)

sudo depmod -a

sudo modprobe xfrm_user
```

Verify:

```bash
python3 - <<'PY'
import socket

for proto, name in [
    (0,  "NETLINK_ROUTE"),
    (6,  "NETLINK_XFRM"),
    (12, "NETLINK_NETFILTER"),
]:
    try:
        s = socket.socket(
            socket.AF_NETLINK,
            socket.SOCK_RAW,
            proto
        )
        print(f"{name}: OK")
        s.close()
    except OSError as e:
        print(
            f"{name}: FAIL "
            f"errno={e.errno} {e}"
        )
PY
```

All three should return:

```text
OK
```

---

## 21.2 Kata works with `--net=none` but fails with normal networking

If:

```bash
sudo nerdctl run \
  -it \
  --rm \
  --net=none \
  --runtime io.containerd.kata.v2 \
  ubuntu:22.04 \
  sh
```

works, but normal networking fails, check the host networking modules first:

```bash
sudo modprobe xfrm_user
sudo modprobe vhost_net
sudo modprobe sch_ingress
sudo modprobe cls_u32
sudo modprobe act_mirred
```

Then verify:

```bash
lsmod | grep -E \
'xfrm_user|vhost_net|tap|sch_ingress|cls_u32|act_mirred'
```

---

## 21.3 CUBIC does not appear inside the guest

Check:

```bash
grep -E \
'CONFIG_TCP_CONG_(CUBIC|BBR)|CONFIG_DEFAULT_(CUBIC|BBR)|CONFIG_DEFAULT_TCP_CONG' \
"$KDIR/.config"
```

Expected:

```text
CONFIG_TCP_CONG_CUBIC=y
CONFIG_TCP_CONG_BBR=y
CONFIG_DEFAULT_CUBIC=y
# CONFIG_DEFAULT_BBR is not set
CONFIG_DEFAULT_TCP_CONG="cubic"
```

Check which guest kernel Kata is actually using:

```bash
readlink -f \
  /opt/kata/share/kata-containers/vmlinuz.container

readlink -f \
  /opt/kata/share/kata-containers/vmlinux.container
```

Also:

```bash
sudo kata-runtime env \
  | grep -i -A5 kernel
```

Then stop any old Kata VM and create a new container.

---

## 21.4 `ubuntu:22.04` does not contain the `ip` command

Install:

```bash
apt update
apt install -y iproute2
```

Alternatively, use BusyBox for a quick host-side CNI test:

```bash
sudo nerdctl run \
  --rm \
  --network kata-net \
  busybox \
  ip addr
```

---

## 21.5 Bash shows a `>` continuation prompt

A trailing:

```text
\
```

means Bash expects another line.

Press:

```text
Ctrl+C
```

to cancel the incomplete command.

---

# Final Verification

## Host

Check:

```bash
uname -r
```

Expected for the tested Raspberry Pi 4:

```text
5.15.0-1105-raspi
```

Verify host networking support:

```bash
lsmod | grep -E \
'xfrm_user|vhost_net|vhost_vsock|tap|sch_ingress|cls_u32|act_mirred'
```

Verify the custom guest kernel:

```bash
readlink -f \
  /opt/kata/share/kata-containers/vmlinuz.container

readlink -f \
  /opt/kata/share/kata-containers/vmlinux.container
```

---

## Kata guest

Run:

```bash
sudo nerdctl run \
  -it \
  --rm \
  --network kata-net \
  --runtime io.containerd.kata.v2 \
  ubuntu:22.04 \
  sh
```

Inside the guest:

```bash
uname -r

sysctl \
  net.ipv4.tcp_congestion_control

cat \
  /proc/sys/net/ipv4/tcp_available_congestion_control
```

Expected:

```text
6.12.47

net.ipv4.tcp_congestion_control = cubic

reno cubic bbr
```

At this point:

```text
RPi4 host kernel       = Linux 5.15
Kata guest kernel      = Linux 6.12.47
Kata networking        = working
Guest CUBIC            = available
Guest BBR              = available
Default guest CCA      = CUBIC
```

The Raspberry Pi 4 Kata environment is ready for the CUBIC-based microVM experiments.
