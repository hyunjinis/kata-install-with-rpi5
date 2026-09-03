# Kata Containers on Raspberry Pi 5 — Full Terminal Log

This document preserves the **actual terminal commands and outputs** recorded while setting up Kata Containers on Raspberry Pi 5.

Unlike the main installation guide, this file keeps verbose package installation, download, kernel setup, compilation, and installation logs for reference and reproducibility.

> **Notation**
>
> - Commands are always visible.
> - Long terminal outputs are hidden inside expandable sections.
> - Click **Show full terminal output** to inspect the recorded output.
> - Kernel compilation logs such as `CC`, `AR`, `LD`, `OBJCOPY`, and `GZIP` are intentionally preserved.

---

# 1. Install Kata Containers

## 1.1 Install and extract Kata Containers 3.24.0

**Command**

```bash
sudo apt update

wget \
  https://github.com/kata-containers/kata-containers/releases/download/3.24.0/kata-static-3.24.0-arm64.tar.zst

sudo tar -xvf \
  kata-static-3.24.0-arm64.tar.zst \
  -C /

rm -f kata-static-3.24.0-arm64.tar.zst
```

<details>
<summary><strong>Show full terminal output</strong></summary>

```text
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done

Hit:1 https://prod-cdn.packages.k8s.io/repositories/isv:/kubernetes:/core:/stable:/v1.28/deb InRelease
Hit:2 http://ports.ubuntu.com/ubuntu-ports noble InRelease
Get:3 http://ports.ubuntu.com/ubuntu-ports noble-backports InRelease
Get:4 http://ports.ubuntu.com/ubuntu-ports noble-security InRelease
Get:5 http://ports.ubuntu.com/ubuntu-ports noble-updates InRelease

...

HTTP request sent, awaiting response... 200 OK
Length: 476813228 (455M) [application/octet-stream]
Saving to: ‘kata-static-3.24.0-arm64.tar.zst’

kata-static-3.24.0-arm64.tar.zst 100%[===================>] 454.72M

./
./opt/
./opt/kata/
./opt/kata/versions.yaml
./opt/kata/share/
./opt/kata/share/kata-containers/
./opt/kata/share/kata-containers/kata-containers.img
./opt/kata/share/kata-containers/vmlinuz.container
./opt/kata/share/kata-containers/vmlinux.container
./opt/kata/share/kata-containers/config-6.12.47-173
./opt/kata/share/kata-containers/vmlinuz-6.12.47-173
./opt/kata/share/kata-containers/vmlinux-6.12.47-173
...
./opt/kata/bin/containerd-shim-kata-v2
./opt/kata/bin/qemu-system-aarch64
./opt/kata/bin/kata-runtime
```

</details>

---

## 1.2 Create Kata command symlinks

**Command**

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

## 1.3 Verify Kata Containers

**Command**

```bash
kata-runtime --version
```

<details>
<summary><strong>Show terminal output</strong></summary>

```text
kata-runtime  : 3.24.0
   commit   : c7d0c270ee7dfaa6d978e6e07b99dabdaf2b9fda
   OCI specs: 1.2.1
```

</details>

---

# 2. Check Host Kernel Support

## 2.1 Load vhost modules

**Command**

```bash
sudo modprobe vhost
sudo modprobe vhost_net
sudo modprobe vhost_vsock
```

Verify:

```bash
lsmod | grep -E 'vhost|vsock|tap'
```

<details>
<summary><strong>Show terminal output</strong></summary>

```text
vhost_vsock            24576  0
vmw_vsock_virtio_transport_common    53248  1 vhost_vsock
vsock                  61440  2 vmw_vsock_virtio_transport_common,vhost_vsock
vhost_net              32768  0
tun                    61440  1 vhost_net
tap                    36864  1 vhost_net
vhost                  69632  2 vhost_vsock,vhost_net
vhost_iotlb            16384  1 vhost
```

</details>

---

## 2.2 Check Kata compatibility

**Command**

```bash
sudo kata-runtime check
```

<details>
<summary><strong>Show terminal output</strong></summary>

```text
WARN[0000] Not running network checks as super user
System is capable of running Kata Containers
System can currently create Kata Containers
```

</details>

---

# 3. Install Guest Kernel Build Dependencies

**Command**

```bash
sudo apt install -y \
  flex \
  bison \
  libelf-dev \
  libncurses-dev
```

<details>
<summary><strong>Show full package installation output</strong></summary>

```text
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done

flex is already the newest version.
bison is already the newest version.

The following additional packages will be installed:
  libncurses6
  libncursesw6
  libtinfo6
  libzstd-dev
  ncurses-base
  ncurses-bin
  ncurses-term
  zlib1g
  zlib1g-dev

The following NEW packages will be installed:
  libelf-dev
  libzstd-dev
  zlib1g-dev

...

Setting up libzstd-dev ...
Setting up libncurses6 ...
Setting up libncursesw6 ...
Setting up zlib1g-dev ...
Setting up ncurses-term ...
Setting up libncurses-dev ...
Setting up libelf-dev ...

Processing triggers for man-db ...
Processing triggers for libc-bin ...
```

</details>

---

# 4. Install Go

## 4.1 Download Go

**Command**

```bash
wget \
  https://go.dev/dl/go1.26.0.linux-arm64.tar.gz
```

<details>
<summary><strong>Show download output</strong></summary>

```text
Resolving go.dev...
Connecting to go.dev...
HTTP request sent, awaiting response... 302 Found

Location: https://dl.google.com/go/go1.26.0.linux-arm64.tar.gz

HTTP request sent, awaiting response... 200 OK
Length: 63655921 (61M)

Saving to: ‘go1.26.0.linux-arm64.tar.gz’

go1.26.0.linux-arm64.tar.gz 100%[===================>] 60.71M
```

</details>

---

## 4.2 Install Go

**Command**

```bash
sudo rm -rf /usr/local/go

sudo tar \
  -C /usr/local \
  -xzf go1.26.0.linux-arm64.tar.gz
```

Configure `PATH`:

```bash
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

<details>
<summary><strong>Show terminal output</strong></summary>

```text
/usr/local/go/bin/go
go version go1.26.0 linux/arm64
```

</details>

---

# 5. Install Rust

**Command**

```bash
curl \
  https://sh.rustup.rs \
  -sSf | sh -s -- -y
```

Load Rust environment:

```bash
source "$HOME/.cargo/env"
```

Verify:

```bash
rustc --version
cargo --version
```

<details>
<summary><strong>Show full Rust installation output</strong></summary>

```text
info: downloading installer
info: profile set to default
info: default host tuple is aarch64-unknown-linux-gnu
info: syncing channel updates for stable-aarch64-unknown-linux-gnu

info: downloading 6 components
cargo installed
clippy installed
rust-docs installed
rust-std installed
rustc installed
rustfmt installed

info: default toolchain set to stable-aarch64-unknown-linux-gnu

stable-aarch64-unknown-linux-gnu installed - rustc 1.98.0

Rust is installed now. Great!

To get started you may need to restart your current shell.
```

</details>

---

# 6. Install yq

**Command**

```bash
go install \
  github.com/mikefarah/yq/v4@v4.52.4
```

Add Go user binaries to `PATH`:

```bash
echo \
  'export PATH=$HOME/go/bin:$PATH' \
  >> ~/.bashrc

source ~/.bashrc
```

Install globally:

```bash
sudo cp \
  "$HOME/go/bin/yq" \
  /usr/local/bin/yq
```

Verify:

```bash
yq --version
```

<details>
<summary><strong>Show full yq installation output</strong></summary>

```text
go: downloading github.com/mikefarah/yq/v4 v4.52.4
go: downloading github.com/spf13/cobra
go: downloading github.com/spf13/pflag
go: downloading gopkg.in/op/go-logging.v1
go: downloading github.com/a8m/envsubst
go: downloading github.com/alecthomas/participle/v2
go: downloading github.com/fatih/color
go: downloading github.com/goccy/go-json
go: downloading github.com/goccy/go-yaml
go: downloading golang.org/x/net
go: downloading golang.org/x/text
go: downloading golang.org/x/sys
...

yq (https://github.com/mikefarah/yq/) version v4.52.4
```

</details>

---

# 7. Clone Kata Containers

**Command**

```bash
git clone \
  https://github.com/kata-containers/kata-containers.git \
  ~/kata-containers
```

<details>
<summary><strong>Show Git clone output</strong></summary>

```text
Cloning into '/home/rpi3/kata-containers'...

remote: Enumerating objects: ...
remote: Counting objects: 100% ...
remote: Compressing objects: 100% ...

Receiving objects: 100% ...
Resolving deltas: 100% ...
```

</details>

---

# 8. Prepare Kata Guest Kernel

Move to the kernel packaging directory:

```bash
cd \
  ~/kata-containers/tools/packaging/kernel
```

Run setup:

```bash
./build-kernel.sh \
  -a aarch64 \
  -v 6.12.47 \
  -f \
  -d \
  setup
```

<details>
<summary><strong>Show full kernel setup output</strong></summary>

```text
Line 623: getopts a:b:c:dD:eEfg:hH:k:mp:r:st:u:v:x opt
Line 695: shift 6
Line 697: subcmd=setup

Line 737: kernel_version=6.12.47
Line 740: get_config_version

INFO: Config version: 182
INFO: Kernel version: 6.12.47

INFO: kernel path does not exist, will download kernel

INFO: Download kernel checksum file:
https://cdn.kernel.org/pub/linux/kernel/v6.x/sha256sums.asc

100 198k 100 198k ...

INFO: sha256sums.asc is valid,
linux-6.12.47.tar.xz.sha256 generated

INFO: Download kernel version 6.12.47

INFO: Download kernel from:
https://www.kernel.org/pub/linux/kernel/v6.x/linux-6.12.47.tar.xz

100 141M 100 141M ...

linux-6.12.47.tar.xz: OK

INFO: Apply patches from ...
INFO: Found 0 patches

INFO: Constructing config from fragments:
...
```

</details>

---

# 9. Enable CUBIC and BBR

Determine the current Kata kernel config revision:

```bash
cd \
  ~/kata-containers/tools/packaging/kernel

CFG=$(cat kata_config_version)

KDIR="$PWD/kata-linux-6.12.47-$CFG"

echo "CFG=$CFG"
echo "KDIR=$KDIR"
```

<details>
<summary><strong>Show terminal output</strong></summary>

```text
CFG=202
KDIR=/home/rpi3/kata-containers/tools/packaging/kernel/kata-linux-6.12.47-202
```

</details>

Enable CUBIC and BBR:

```bash
"$KDIR/scripts/config" \
  --file "$KDIR/.config" \
  -e TCP_CONG_CUBIC \
  -e TCP_CONG_BBR \
  -e DEFAULT_CUBIC \
  -d DEFAULT_BBR
```

Resolve dependencies:

```bash
make \
  -C "$KDIR" \
  ARCH=arm64 \
  olddefconfig
```

Verify:

```bash
grep -E \
'CONFIG_TCP_CONG_(CUBIC|BBR)|CONFIG_DEFAULT_(CUBIC|BBR)|CONFIG_DEFAULT_TCP_CONG' \
"$KDIR/.config"
```

<details>
<summary><strong>Show terminal output</strong></summary>

```text
CONFIG_TCP_CONG_CUBIC=y
CONFIG_TCP_CONG_BBR=y
CONFIG_DEFAULT_CUBIC=y
# CONFIG_DEFAULT_BBR is not set
CONFIG_DEFAULT_TCP_CONG="cubic"
```

</details>

---

# 10. Build the Kata Guest Kernel

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

<details>
<summary><strong>Show full kernel compilation log</strong></summary>

```text
INFO: Config version: 202
INFO: Kernel version: 6.12.47

  SYNC    include/config/auto.conf.cmd
  CALL    scripts/checksyscalls.sh
  DESCEND objtool

  CC      init/main.o
  CC      init/do_mounts.o
  CC      init/noinitramfs.o

  CC      kernel/fork.o
  CC      kernel/exec_domain.o
  CC      kernel/panic.o
  CC      kernel/cpu.o

  CC      net/core/sock.o
  CC      net/core/request_sock.o
  CC      net/core/skbuff.o
  CC      net/core/datagram.o

  CC      net/ipv4/route.o
  CC      net/ipv4/inetpeer.o
  CC      net/ipv4/protocol.o
  CC      net/ipv4/ip_input.o
  CC      net/ipv4/ip_fragment.o
  CC      net/ipv4/ip_forward.o
  CC      net/ipv4/ip_options.o
  CC      net/ipv4/ip_output.o
  CC      net/ipv4/ip_sockglue.o
  CC      net/ipv4/inet_hashtables.o
  CC      net/ipv4/inet_timewait_sock.o
  CC      net/ipv4/inet_connection_sock.o

  CC      net/ipv4/tcp.o
  CC      net/ipv4/tcp_input.o
  CC      net/ipv4/tcp_output.o
  CC      net/ipv4/tcp_timer.o
  CC      net/ipv4/tcp_ipv4.o
  CC      net/ipv4/tcp_minisocks.o
  CC      net/ipv4/tcp_cong.o
  CC      net/ipv4/tcp_cubic.o
  CC      net/ipv4/tcp_bbr.o

  CC      drivers/firmware/efi/libstub/efi-stub-helper.o
  CC      net/netfilter/nf_conntrack_helper.o
  CC      net/ipv6/udplite.o
  CC      drivers/firmware/efi/libstub/gop.o
  CC      net/ipv6/raw.o
  CC      net/ipv4/fib_semantics.o
  CC      net/netfilter/nf_conntrack_proto.o
  CC      drivers/firmware/efi/libstub/secureboot.o
  CC      drivers/firmware/efi/libstub/tpm.o
  CC      net/netfilter/nf_conntrack_proto_generic.o
  CC      drivers/firmware/efi/libstub/file.o
  CC      net/ipv6/icmp.o
  CC      net/ipv4/fib_trie.o
  CC      drivers/firmware/efi/libstub/mem.o
  CC      net/netfilter/nf_conntrack_proto_tcp.o
  CC      drivers/firmware/efi/libstub/random.o
  CC      net/ipv6/mcast.o
  CC      drivers/firmware/efi/libstub/randomalloc.o
  CC      drivers/firmware/efi/libstub/pci.o
  CC      net/netfilter/nf_conntrack_proto_udp.o
  CC      net/ipv4/fib_notifier.o
  CC      drivers/firmware/efi/libstub/skip_spaces.o
  CC      drivers/firmware/efi/libstub/lib-cmdline.o
  CC      drivers/firmware/efi/libstub/lib-ctype.o
  CC      drivers/firmware/efi/libstub/alignedmem.o
  CC      net/ipv4/inet_fragment.o
  CC      drivers/firmware/efi/libstub/relocate.o
  CC      net/netfilter/nf_conntrack_proto_icmp.o

  CC      net/netfilter/xt_iprange.o
  CC      net/netfilter/xt_ipvs.o
  CC      net/netfilter/xt_l2tp.o
  CC      net/netfilter/xt_length.o
  CC      net/netfilter/xt_limit.o
  CC      net/netfilter/xt_mac.o
  CC      net/netfilter/xt_multiport.o
  CC      net/netfilter/xt_nfacct.o
  CC      net/netfilter/xt_osf.o
  CC      net/netfilter/xt_owner.o
  CC      net/netfilter/xt_cgroup.o
  CC      net/netfilter/xt_physdev.o
  CC      net/netfilter/xt_pkttype.o
  CC      net/netfilter/xt_policy.o
  CC      net/netfilter/xt_quota.o
  CC      net/netfilter/xt_rateest.o
  CC      net/netfilter/xt_realm.o
  CC      net/netfilter/xt_recent.o
  CC      net/netfilter/xt_sctp.o
  CC      net/netfilter/xt_state.o
  CC      net/netfilter/xt_statistic.o
  CC      net/netfilter/xt_string.o
  CC      net/netfilter/xt_tcpmss.o
  CC      net/netfilter/xt_time.o
  CC      net/netfilter/xt_u32.o

  AR      net/netfilter/built-in.a
  AR      net/built-in.a
  AR      built-in.a
  AR      vmlinux.a

  LD      vmlinux.o

  OBJCOPY modules.builtin.modinfo
  GEN     modules.builtin
  MODPOST vmlinux.symvers
  UPD     include/generated/utsversion.h

  CC      init/version-timestamp.o

  KSYMS   .tmp_vmlinux0.kallsyms.S
  AS      .tmp_vmlinux0.kallsyms.o
  LD      .tmp_vmlinux1
  NM      .tmp_vmlinux1.syms

  KSYMS   .tmp_vmlinux1.kallsyms.S
  AS      .tmp_vmlinux1.kallsyms.o
  LD      .tmp_vmlinux2
  NM      .tmp_vmlinux2.syms

  KSYMS   .tmp_vmlinux2.kallsyms.S
  AS      .tmp_vmlinux2.kallsyms.o

  LD      vmlinux
  NM      System.map
  SORTTAB vmlinux

  OBJCOPY arch/arm64/boot/Image
  GZIP    arch/arm64/boot/Image.gz
```

> The actual compilation log is much longer.  
> The complete recorded output can be placed inside this block without affecting the readability of the main document.

</details>

---

# 11. Verify Kernel Build Artifacts

**Command**

```bash
ls -lh "$KDIR/vmlinux"

ls -lh \
  "$KDIR/arch/arm64/boot/Image"

ls -lh \
  "$KDIR/arch/arm64/boot/Image.gz"
```

<details>
<summary><strong>Show terminal output</strong></summary>

```text
-rwxr-xr-x ... vmlinux
-rw-r--r-- ... arch/arm64/boot/Image
-rw-r--r-- ... arch/arm64/boot/Image.gz
```

</details>

---

# 12. Install the Kata Guest Kernel

**Command**

```bash
sudo ./build-kernel.sh \
  -a aarch64 \
  -v 6.12.47 \
  -d \
  install
```

<details>
<summary><strong>Show full kernel installation output</strong></summary>

```text
INFO: Config version: 202
INFO: Kernel version: 6.12.47

install_path=/usr/share/kata-containers

vmlinuz=vmlinuz-6.12.47-202
vmlinux=vmlinux-6.12.47-202

install --mode 0644 -D \
  arch/arm64/boot/Image.gz \
  /usr/share/kata-containers/vmlinuz-6.12.47-202

install --mode 0644 -D \
  arch/arm64/boot/Image \
  /usr/share/kata-containers/vmlinux-6.12.47-202

install --mode 0644 -D \
  ./.config \
  /usr/share/kata-containers/config-6.12.47-202

ln -sf \
  vmlinuz-6.12.47-202 \
  /usr/share/kata-containers/vmlinuz.container

ln -sf \
  vmlinux-6.12.47-202 \
  /usr/share/kata-containers/vmlinux.container

lrwxrwxrwx ... vmlinux.container -> vmlinux-6.12.47-202
lrwxrwxrwx ... vmlinuz.container -> vmlinuz-6.12.47-202
```

</details>

---

# 13. Copy the Custom Kernel into Static Kata

**Command**

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

Update symlinks:

```bash
cd \
  /opt/kata/share/kata-containers

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

<details>
<summary><strong>Show terminal output</strong></summary>

```text
/opt/kata/share/kata-containers/vmlinuz-6.12.47-202
/opt/kata/share/kata-containers/vmlinux-6.12.47-202
```

</details>

---

# 14. Verify CNI Plugins

**Command**

```bash
ls /opt/cni/bin/
```

<details>
<summary><strong>Show terminal output</strong></summary>

```text
bandwidth
bridge
dhcp
dummy
firewall
flannel
host-device
host-local
ipvlan
loopback
macvlan
portmap
ptp
sbr
static
tuning
vlan
vrf
```

</details>

Check the bridge plugin:

```bash
/opt/cni/bin/bridge \
  2>&1 | head -3
```

<details>
<summary><strong>Show terminal output</strong></summary>

```text
CNI bridge plugin v1.2.0
CNI protocol versions supported:
0.1.0, 0.2.0, 0.3.0, 0.3.1, 0.4.0, 1.0.0
```

</details>

---

# 15. Check containerd CNI Configuration

**Command**

```bash
containerd config dump \
  | grep -i cni
```

<details>
<summary><strong>Show terminal output</strong></summary>

```text
[plugins."io.containerd.grpc.v1.cri".cni]
  bin_dir = "/opt/cni/bin"
  conf_dir = "/etc/cni/net.d"

...

"cniconfig": {
    "PluginDirs": [
        "/opt/cni/bin"
    ],
    "PluginConfDir": "/etc/cni/net.d"
}

...

"lastCNILoadStatus": "OK"
"lastCNILoadStatus.default": "OK"
```

</details>

---

# 16. Configure containerd for Kata

Back up the existing configuration:

```bash
sudo cp \
  /etc/containerd/config.toml \
  /etc/containerd/config.toml.bak
```

Edit:

```bash
sudo nano \
  /etc/containerd/config.toml
```

Example Kata runtime configuration:

```toml
[plugins."io.containerd.cri.v1.runtime".containerd.runtimes.runc]
  runtime_type = "io.containerd.runc.v2"

  [plugins."io.containerd.cri.v1.runtime".containerd.runtimes.runc.options]
    SystemdCgroup = true

[plugins."io.containerd.cri.v1.runtime".containerd.runtimes.kata]
  runtime_type = "io.containerd.kata.v2"
```

Restart containerd:

```bash
sudo systemctl restart containerd
```

---

# 17. Configure CNI Network

**Command**

```bash
sudo tee \
  /etc/cni/net.d/10-mynet.conf \
  > /dev/null <<'EOF'
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
cat \
  /etc/cni/net.d/10-mynet.conf
```

---

# 18. Install nerdctl

**Command**

```bash
wget \
  https://github.com/containerd/nerdctl/releases/download/v2.2.1/nerdctl-2.2.1-linux-arm64.tar.gz

tar xzvf \
  nerdctl-2.2.1-linux-arm64.tar.gz

sudo cp \
  nerdctl \
  /usr/local/bin/nerdctl
```

Verify:

```bash
nerdctl --version
```

<details>
<summary><strong>Show terminal output</strong></summary>

```text
nerdctl version 2.2.1
```

</details>

---

# 19. Run Kata Containers

**Command**

```bash
sudo nerdctl run \
  -it \
  --rm \
  --runtime io.containerd.kata.v2 \
  ubuntu:22.04 \
  sh
```

<details>
<summary><strong>Show startup output</strong></summary>

```text
WARN[0000] cannot set cgroup manager to "systemd" for runtime "io.containerd.kata.v2"

#
```

</details>

---

# 20. Verify Guest Kernel

Run inside the Kata guest.

```bash
uname -r
```

<details>
<summary><strong>Show terminal output</strong></summary>

```text
6.12.47
```

</details>

---

# 21. Verify CUBIC

**Command**

```bash
sysctl \
  net.ipv4.tcp_congestion_control
```

<details>
<summary><strong>Show terminal output</strong></summary>

```text
net.ipv4.tcp_congestion_control = cubic
```

</details>

Check available CCAs:

```bash
cat \
  /proc/sys/net/ipv4/tcp_available_congestion_control
```

<details>
<summary><strong>Show terminal output</strong></summary>

```text
reno cubic bbr
```

</details>

---

# 22. Verify Guest Networking

Install networking tools:

```bash
apt update

apt install -y \
  iproute2 \
  iputils-ping
```

<details>
<summary><strong>Show full package installation output</strong></summary>

```text
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done

The following additional packages will be installed:
  libatm1
  libbpf0
  libbsd0
  libcap2-bin
  libelf1
  libmd0
  libmnl0
  libpam-cap
  libxtables12

...

Setting up iproute2 ...
Setting up iputils-ping ...
```

</details>

Check network interfaces:

```bash
ip addr
```

<details>
<summary><strong>Show terminal output</strong></summary>

```text
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536
    inet 127.0.0.1/8 scope host lo

2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500
    inet 10.x.x.x/24 scope global eth0
```

</details>

Check route:

```bash
ip route
```

Check Internet connectivity:

```bash
ping -c 3 \
  1.1.1.1
```

<details>
<summary><strong>Show ping output</strong></summary>

```text
PING 1.1.1.1 (1.1.1.1): 56 data bytes

64 bytes from 1.1.1.1: icmp_seq=1 ...
64 bytes from 1.1.1.1: icmp_seq=2 ...
64 bytes from 1.1.1.1: icmp_seq=3 ...

--- 1.1.1.1 ping statistics ---
3 packets transmitted, 3 packets received, 0% packet loss
```

</details>

---

# 23. Final Verification

## Host

```bash
kata-runtime --version
```

```bash
readlink -f \
  /opt/kata/share/kata-containers/vmlinuz.container
```

```bash
readlink -f \
  /opt/kata/share/kata-containers/vmlinux.container
```

---

## Kata Guest

```bash
uname -r
```

```bash
sysctl \
  net.ipv4.tcp_congestion_control
```

```bash
cat \
  /proc/sys/net/ipv4/tcp_available_congestion_control
```

Expected:

```text
Kata Containers      3.24.0
Guest kernel         6.12.47
Default CCA          cubic
Available CCAs       reno cubic bbr
```

At this point, the Kata guest kernel supports both **CUBIC** and **BBR**, with **CUBIC configured as the default TCP congestion-control algorithm**.
