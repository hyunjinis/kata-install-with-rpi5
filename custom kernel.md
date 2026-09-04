# Modify and Switch the Kata Guest Kernel on Raspberry Pi

This document describes how to:

1. Prepare the Kata Containers guest-kernel source.
2. Reuse the existing **CUBIC-enabled kernel configuration**.
3. Modify the guest kernel with the **Pre-GSO implementation**.
4. Build and install the modified guest kernel.
5. Verify that the modified kernel is actually used by Kata.
6. Verify that **CUBIC** is still enabled.
7. Switch between the **baseline CUBIC kernel** and the **Pre-GSO CUBIC kernel** without rebuilding.

> **Environment**
>
> * Kata Containers: `3.24.0`
> * Architecture: `aarch64`
> * Guest kernel: `Linux 6.12.47`
> * Kata installation path: `/opt/kata`
> * Baseline CUBIC kernel: `vmlinux-6.12.47-202`
> * Pre-GSO CUBIC kernel: `vmlinux-6.12.47-custom-cubic`

---

# 1. Check the Current Kata Runtime

## 1.1 Check Kata version

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

Also verify the binary installed under `/opt/kata`.

```bash
/opt/kata/bin/kata-runtime --version
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

# 2. Check the Kata Guest-Kernel Path

## 2.1 Check configuration paths

**Command**

```bash
kata-runtime --show-default-config-paths
```

<details>
<summary><strong>Show terminal output</strong></summary>

```text
/etc/kata-containers/configuration.toml
/opt/kata/share/defaults/kata-containers/configuration.toml
```

</details>

---

## 2.2 Check the configured kernel path

**Command**

```bash
sudo grep -R \
'^[[:space:]]*kernel[[:space:]]*=' \
/etc/kata-containers \
/usr/share/defaults/kata-containers \
/opt/kata/share/defaults/kata-containers \
2>/dev/null
```

<details>
<summary><strong>Show relevant terminal output</strong></summary>

```text
/opt/kata/share/defaults/kata-containers/configuration-qemu.toml:
kernel = "/opt/kata/share/kata-containers/vmlinux.container"

/opt/kata/share/defaults/kata-containers/configuration.toml:
kernel = "/opt/kata/share/kata-containers/vmlinux.container"

/opt/kata/share/defaults/kata-containers/configuration-fc.toml:
kernel = "/opt/kata/share/kata-containers/vmlinux.container"
```

</details>

Therefore, the guest kernel actually used by this Kata installation is selected through:

```text
/opt/kata/share/kata-containers/vmlinux.container
```

---

# 3. Check the Currently Selected Kernel

**Command**

```bash
readlink -f \
/opt/kata/share/kata-containers/vmlinux.container
```

Before applying Pre-GSO, the CUBIC baseline kernel was:

<details>
<summary><strong>Show terminal output</strong></summary>

```text
/opt/kata/share/kata-containers/vmlinux-6.12.47-202
```

</details>

Check the symbolic link:

```bash
ls -lh \
/opt/kata/share/kata-containers/vmlinux.container
```

<details>
<summary><strong>Show terminal output</strong></summary>

```text
lrwxrwxrwx 1 root root 19 Sep 3 16:33 \
/opt/kata/share/kata-containers/vmlinux.container \
-> vmlinux-6.12.47-202
```

</details>

---

# 4. Check the Available Guest Kernels

**Command**

```bash
ls -lh \
/opt/kata/share/kata-containers/
```

<details>
<summary><strong>Show relevant terminal output</strong></summary>

```text
-rw-r--r-- 1 root root  89K Dec  5  2025 config-6.12.47-173
-rw-r--r-- 1 root root  92K Sep  3 16:32 config-6.12.47-202

-rw-r--r-- 1 root root  15M Dec  5  2025 vmlinux-6.12.47-173
-rw-r--r-- 1 root root  17M Sep  3 16:32 vmlinux-6.12.47-202

lrwxrwxrwx 1 root root   19 Sep  3 16:33 vmlinux.container \
-> vmlinux-6.12.47-202

lrwxrwxrwx 1 root root   19 Dec  5  2025 vmlinux.container.bak \
-> vmlinux-6.12.47-173

-rw-r--r-- 1 root root 6.6M Dec  5  2025 vmlinuz-6.12.47-173
-rw-r--r-- 1 root root 7.5M Sep  3 16:32 vmlinuz-6.12.47-202
```

</details>

The kernels used in the revised experiment are:

```text
vmlinux-6.12.47-202
    CUBIC baseline kernel
    Pre-GSO OFF

vmlinux-6.12.47-custom-cubic
    Modified guest kernel
    Pre-GSO ON
```

The original Kata kernel:

```text
vmlinux-6.12.47-173
```

is kept only as the original installation backup.

---

# 5. Verify CUBIC in the Baseline Kernel

The CUBIC baseline configuration is:

```text
/opt/kata/share/kata-containers/config-6.12.47-202
```

Check the TCP congestion-control configuration.

**Command**

```bash
grep -E \
'CONFIG_TCP_CONG_CUBIC|CONFIG_TCP_CONG_BBR|CONFIG_DEFAULT_CUBIC|CONFIG_DEFAULT_BBR|CONFIG_DEFAULT_TCP_CONG' \
/opt/kata/share/kata-containers/config-6.12.47-202
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

This means:

```text
CUBIC = built-in
BBR   = built-in
Default TCP congestion control = CUBIC
```

---

# 6. Back Up the Existing CUBIC Kernel

Before modifying the guest kernel, back up the existing CUBIC baseline.

**Command**

```bash
mkdir -p \
~/kata_kernel_backup
```

```bash
sudo cp -a \
/opt/kata/share/kata-containers/vmlinux-6.12.47-202 \
~/kata_kernel_backup/
```

```bash
sudo cp -a \
/opt/kata/share/kata-containers/config-6.12.47-202 \
~/kata_kernel_backup/
```

Save the original symbolic-link information.

```bash
ls -l \
/opt/kata/share/kata-containers/vmlinux.container \
| tee \
~/kata_kernel_backup/original_link.txt
```

<details>
<summary><strong>Show terminal output</strong></summary>

```text
lrwxrwxrwx 1 root root 19 Sep 3 16:33 \
/opt/kata/share/kata-containers/vmlinux.container \
-> vmlinux-6.12.47-202
```

</details>

---

# 7. Clone the Exact Kata Containers Version

Create a separate directory for the modified guest kernel.

**Command**

```bash
cd ~

mkdir -p \
kata_guest_custom

cd \
kata_guest_custom
```

Clone Kata Containers `3.24.0`.

```bash
git clone \
--branch 3.24.0 \
--depth 1 \
https://github.com/kata-containers/kata-containers.git
```

<details>
<summary><strong>Show full Git clone output</strong></summary>

```text
Cloning into 'kata-containers'...

remote: Enumerating objects: 8429, done.
remote: Counting objects: 100% (8429/8429), done.
remote: Compressing objects: 100% (6633/6633), done.
remote: Total 8429 (delta 1873), reused 5105 (delta 1301), pack-reused 0 (from 0)

Receiving objects: 100% (8429/8429), 18.03 MiB | 24.32 MiB/s, done.
Resolving deltas: 100% (1873/1873), done.

Note: switching to 'c7d0c270ee7dfaa6d978e6e07b99dabdaf2b9fda'.

You are in 'detached HEAD' state.
```

</details>

The commit should match the installed Kata runtime:

```text
c7d0c270ee7dfaa6d978e6e07b99dabdaf2b9fda
```

---

# 8. Move to the Guest-Kernel Build Directory

**Command**

```bash
cd \
~/kata_guest_custom/kata-containers/tools/packaging/kernel
```

Check the directory.

```bash
ls
```

<details>
<summary><strong>Show terminal output</strong></summary>

```text
README.md
build-kernel.sh
configs
kata_config_version
patches
```

</details>

Check the config revision associated with the Kata 3.24.0 source.

```bash
cat \
kata_config_version
```

<details>
<summary><strong>Show terminal output</strong></summary>

```text
173
```

</details>

> `173` is the config revision associated with the checked-out Kata 3.24.0 source tree.
>
> The existing CUBIC configuration from `config-6.12.47-202` is explicitly reused in the following step.

---

# 9. Prepare the Guest-Kernel Source with the Existing CUBIC Configuration

Use Linux `6.12.47` and the existing CUBIC-enabled configuration.

**Command**

```bash
./build-kernel.sh \
-a aarch64 \
-v 6.12.47 \
-c /opt/kata/share/kata-containers/config-6.12.47-202 \
setup
```

After setup, the source directory is:

```text
kata-linux-6.12.47-173
```

The source tree is located at:

```text
~/kata_guest_custom/kata-containers/tools/packaging/kernel/kata-linux-6.12.47-173
```

> Do not interpret the `-173` directory suffix as the TCP configuration.
>
> The `.config` inside this tree was initialized using the explicitly supplied:
>
> ```text
> config-6.12.47-202
> ```

---

# 10. Verify the Guest-Kernel Source Before Modification

Move into the kernel source tree.

**Command**

```bash
cd \
~/kata_guest_custom/kata-containers/tools/packaging/kernel/kata-linux-6.12.47-173
```

Check the Linux kernel version.

```bash
make -s \
kernelversion
```

Expected:

```text
6.12.47
```

---

## 10.1 Verify CUBIC

**Command**

```bash
grep -E \
'CONFIG_TCP_CONG_CUBIC|CONFIG_TCP_CONG_BBR|CONFIG_DEFAULT_CUBIC|CONFIG_DEFAULT_BBR|CONFIG_DEFAULT_TCP_CONG' \
.config
```

Expected:

```text
CONFIG_TCP_CONG_CUBIC=y
CONFIG_TCP_CONG_BBR=y
CONFIG_DEFAULT_CUBIC=y
# CONFIG_DEFAULT_BBR is not set
CONFIG_DEFAULT_TCP_CONG="cubic"
```

At this point:

```text
Guest kernel = Linux 6.12.47
Default CCA  = CUBIC
Pre-GSO      = not yet applied
```

---

# 11. Modify the Kata Guest Kernel

The directory below is the actual Linux guest-kernel source used to build the Kata custom kernel.

```text
~/kata_guest_custom/kata-containers/tools/packaging/kernel/kata-linux-6.12.47-173/
```

Example source-tree structure:

```text
kata-linux-6.12.47-173/
├── arch/
├── drivers/
├── include/
├── kernel/
├── net/
└── ...
```

Modify the files required by the Pre-GSO implementation.

For example:

```bash
cd \
~/kata_guest_custom/kata-containers/tools/packaging/kernel/kata-linux-6.12.47-173
```

```bash
vim \
net/ipv4/<MODIFIED_FILE>.c
```

or:

```bash
vim \
net/core/<MODIFIED_FILE>.c
```

or:

```bash
vim \
include/linux/<MODIFIED_HEADER>.h
```

Insert the same Pre-GSO implementation used in the original experiment.

> Replace `<MODIFIED_FILE>` and `<MODIFIED_HEADER>` with the actual files modified by the implementation.

---

# 12. Verify that the Modified Code Exists

Before compiling, verify that the Pre-GSO implementation exists in the guest-kernel source.

If the implementation contains a unique function:

```bash
grep -Rni \
"<PRE_GSO_FUNCTION_NAME>" \
net/ \
include/
```

If it contains a unique variable:

```bash
grep -Rni \
"<PRE_GSO_VARIABLE_NAME>" \
net/ \
include/
```

It is also recommended to include an identifiable comment in the modified source:

```c
/* Pre-GSO experimental implementation */
```

Then verify it using:

```bash
grep -Rni \
"Pre-GSO experimental implementation" \
net/ \
include/
```

Example output:

```text
net/ipv4/<MODIFIED_FILE>.c:1234: /* Pre-GSO experimental implementation */
```

---

# 13. Verify CUBIC Again after Modifying the Source

Kernel source changes must not accidentally change the CCA configuration.

**Command**

```bash
grep -E \
'CONFIG_TCP_CONG_CUBIC|CONFIG_TCP_CONG_BBR|CONFIG_DEFAULT_CUBIC|CONFIG_DEFAULT_BBR|CONFIG_DEFAULT_TCP_CONG' \
.config
```

Expected:

```text
CONFIG_TCP_CONG_CUBIC=y
CONFIG_TCP_CONG_BBR=y
CONFIG_DEFAULT_CUBIC=y
# CONFIG_DEFAULT_BBR is not set
CONFIG_DEFAULT_TCP_CONG="cubic"
```

---

# 14. Important: Do Not Run `setup` Again

After modifying the source, do **not** execute:

```bash
./build-kernel.sh \
-a aarch64 \
-v 6.12.47 \
setup
```

and especially do not execute:

```bash
./build-kernel.sh \
-a aarch64 \
-v 6.12.47 \
-f \
setup
```

The setup step can recreate the source tree and remove the manual modifications.

The correct workflow is:

```text
setup
  ↓
modify source
  ↓
verify source
  ↓
build
```

---

# 15. Build the Modified Guest Kernel

Move back to the Kata kernel packaging directory.

**Command**

```bash
cd \
~/kata_guest_custom/kata-containers/tools/packaging/kernel
```

Build the exact modified source tree.

```bash
./build-kernel.sh \
-a aarch64 \
-v 6.12.47 \
-k "$(pwd)/kata-linux-6.12.47-173" \
build
```

The kernel compilation will produce:

```text
vmlinux
arch/arm64/boot/Image
arch/arm64/boot/Image.gz
```

---

# 16. Verify the Kernel Build Artifacts

Move into the source directory.

```bash
cd \
kata-linux-6.12.47-173
```

Check the build artifacts.

```bash
ls -lh \
arch/arm64/boot/Image

ls -lh \
arch/arm64/boot/Image.gz

ls -lh \
vmlinux
```

<details>
<summary><strong>Show actual terminal output</strong></summary>

```text
-rw-rw-r-- 1 rpi3 rpi3 17M Sep 3 17:51 arch/arm64/boot/Image
-rw-rw-r-- 1 rpi3 rpi3 7.5M Sep 3 17:51 arch/arm64/boot/Image.gz
-rwxrwxr-x 1 rpi3 rpi3 20M Sep 3 17:51 vmlinux
```

</details>

Check the kernel release.

```bash
make -s \
kernelrelease
```

<details>
<summary><strong>Show terminal output</strong></summary>

```text
6.12.47
```

</details>

Both the baseline and Pre-GSO kernels report the same kernel release:

```text
6.12.47
```

Therefore, `uname -r` alone cannot distinguish the two kernels.

---

# 17. Copy the Pre-GSO Kernel into the Kata Installation

The ARM64 kernel image used as the uncompressed Kata guest kernel is:

```text
arch/arm64/boot/Image
```

Copy it under a separate name.

**Command**

```bash
sudo cp \
arch/arm64/boot/Image \
/opt/kata/share/kata-containers/vmlinux-6.12.47-custom-cubic
```

Copy the corresponding config.

```bash
sudo cp \
.config \
/opt/kata/share/kata-containers/config-6.12.47-custom-cubic
```

Verify.

```bash
ls -lh \
/opt/kata/share/kata-containers/ \
| grep custom-cubic
```

<details>
<summary><strong>Show actual terminal output</strong></summary>

```text
-rw-r--r-- 1 root root 92K Sep 3 17:55 config-6.12.47-custom-cubic
-rw-r--r-- 1 root root 17M Sep 3 17:55 vmlinux-6.12.47-custom-cubic
```

</details>

The baseline kernel remains unchanged:

```text
/opt/kata/share/kata-containers/vmlinux-6.12.47-202
```

---

# 18. Switch Kata to the Pre-GSO Kernel

Move to the Kata kernel directory.

```bash
cd \
/opt/kata/share/kata-containers
```

Update the symbolic link.

```bash
sudo ln -sfn \
vmlinux-6.12.47-custom-cubic \
vmlinux.container
```

Check the link.

```bash
ls -l \
vmlinux.container
```

<details>
<summary><strong>Show actual terminal output</strong></summary>

```text
lrwxrwxrwx 1 root root 28 Sep 3 17:55 \
vmlinux.container -> vmlinux-6.12.47-custom-cubic
```

</details>

Resolve the actual path.

```bash
readlink -f \
vmlinux.container
```

<details>
<summary><strong>Show actual terminal output</strong></summary>

```text
/opt/kata/share/kata-containers/vmlinux-6.12.47-custom-cubic
```

</details>

---

# 19. Verify that Kata Runtime Selects the Custom Kernel

**Command**

```bash
sudo kata-runtime env \
| grep -A5 '\[Kernel\]'
```

<details>
<summary><strong>Show actual terminal output</strong></summary>

```text
[Kernel]

  Path = "/opt/kata/share/kata-containers/vmlinux-6.12.47-custom-cubic"

  Parameters = "systemd.unit=kata-containers.target systemd.mask=systemd-networkd.service systemd.mask=systemd-networkd.socket scsi_mod.scan=none agent.cdh_api_timeout=50 cgroup_no_v1=all systemd.unified_cgroup_hierarchy=1"

[Meta]

  Version = "1.0.27"
```

</details>

This is the most important host-side verification.

---

# 20. Restart containerd

After changing the guest-kernel link:

```bash
sudo systemctl restart \
containerd
```

Verify:

```bash
sudo systemctl status \
containerd \
--no-pager
```

<details>
<summary><strong>Show actual terminal output</strong></summary>

```text
● containerd.service - containerd container runtime
     Loaded: loaded (/usr/lib/systemd/system/containerd.service; enabled; preset: enabled)
     Active: active (running) since Thu 2026-09-03 17:56:01 KST
       Docs: https://containerd.io
   Main PID: 118373 (containerd)
      Tasks: 221
     Memory: 747.2M
        CPU: 1.065s

Sep 03 17:56:00 rpi3-desktop containerd[118373]: Start subscribing containerd event
Sep 03 17:56:00 rpi3-desktop containerd[118373]: Start recovering state
Sep 03 17:56:00 rpi3-desktop containerd[118373]: serving... address=/run/containerd/containerd.sock
Sep 03 17:56:01 rpi3-desktop containerd[118373]: Start event monitor
Sep 03 17:56:01 rpi3-desktop containerd[118373]: Start cni network conf syncer for default
Sep 03 17:56:01 rpi3-desktop containerd[118373]: Start streaming server
Sep 03 17:56:01 rpi3-desktop systemd[1]: Started containerd.service - containerd container runtime.
Sep 03 17:56:01 rpi3-desktop containerd[118373]: containerd successfully booted
```

</details>

---

# 21. Recreate the Kata Container

An already-running Kata microVM continues using the kernel with which it was originally booted.

Therefore, the existing container must be removed.

```bash
sudo nerdctl rm -f \
kata-test
```

Create a new Kata container using the experiment image.

```bash
sudo nerdctl run -d \
--name kata-test \
--runtime io.containerd.kata.v2 \
jjong2/all:latest \
sleep infinity
```

Verify:

```bash
sudo nerdctl ps
```

Example:

```text
CONTAINER ID    IMAGE                         COMMAND           STATUS    NAMES
xxxxxxxxxxxx    docker.io/jjong2/all:latest   "sleep infinity"  Up        kata-test
```

---

# 22. Verify Required Experiment Tools

Check the tools inside the newly created Kata container.

```bash
sudo nerdctl exec \
kata-test \
which netperf
```

```bash
sudo nerdctl exec \
kata-test \
which vnstat
```

```bash
sudo nerdctl exec \
kata-test \
which mpstat
```

```bash
sudo nerdctl exec \
kata-test \
which pidstat
```

Expected:

```text
/usr/bin/netperf
/usr/bin/vnstat
/usr/bin/mpstat
/usr/bin/pidstat
```

---

# 23. Verify the Guest Kernel

Check the guest kernel release.

```bash
sudo nerdctl exec \
kata-test \
uname -r
```

<details>
<summary><strong>Show terminal output</strong></summary>

```text
6.12.47
```

</details>

Because both the baseline and Pre-GSO kernels report `6.12.47`, verify the actual selected image using:

```bash
sudo kata-runtime env \
| grep -A5 '\[Kernel\]'
```

Expected for Pre-GSO:

```text
Path = "/opt/kata/share/kata-containers/vmlinux-6.12.47-custom-cubic"
```

---

# 24. Verify CUBIC in the Running Kata Guest

Check the currently active congestion-control algorithm.

```bash
sudo nerdctl exec \
kata-test \
sysctl net.ipv4.tcp_congestion_control
```

Expected:

```text
net.ipv4.tcp_congestion_control = cubic
```

Check all available algorithms.

```bash
sudo nerdctl exec \
kata-test \
sysctl net.ipv4.tcp_available_congestion_control
```

<details>
<summary><strong>Show actual terminal output</strong></summary>

```text
net.ipv4.tcp_available_congestion_control = reno bbr cubic
```

</details>

An equivalent direct check is:

```bash
sudo nerdctl exec \
kata-test \
cat /proc/sys/net/ipv4/tcp_congestion_control
```

Expected:

```text
cubic
```

At this point:

```text
Kernel release    = 6.12.47
Kernel image      = vmlinux-6.12.47-custom-cubic
Pre-GSO           = ON
Default CCA       = CUBIC
Available CCAs    = reno bbr cubic
```

---

# 25. Switch Back to the Baseline CUBIC Kernel

The baseline kernel is:

```text
vmlinux-6.12.47-202
```

First remove the running Kata container.

```bash
sudo nerdctl rm -f \
kata-test
```

Move to the Kata guest-kernel directory.

```bash
cd \
/opt/kata/share/kata-containers
```

Change the symbolic link.

```bash
sudo ln -sfn \
vmlinux-6.12.47-202 \
vmlinux.container
```

Verify:

```bash
readlink -f \
vmlinux.container
```

Expected:

```text
/opt/kata/share/kata-containers/vmlinux-6.12.47-202
```

Restart containerd.

```bash
sudo systemctl restart \
containerd
```

Create a new Kata container.

```bash
sudo nerdctl run -d \
--name kata-test \
--runtime io.containerd.kata.v2 \
jjong2/all:latest \
sleep infinity
```

Check the selected kernel.

```bash
sudo kata-runtime env \
| grep -A5 '\[Kernel\]'
```

Expected:

```text
[Kernel]

  Path = "/opt/kata/share/kata-containers/vmlinux-6.12.47-202"
```

Verify CUBIC.

```bash
sudo nerdctl exec \
kata-test \
sysctl net.ipv4.tcp_congestion_control
```

Expected:

```text
net.ipv4.tcp_congestion_control = cubic
```

This configuration is:

```text
Pre-GSO = OFF
CUBIC   = ON
```

---

# 26. Switch Back to the Pre-GSO Kernel

Remove the baseline Kata VM.

```bash
sudo nerdctl rm -f \
kata-test
```

Move to:

```bash
cd \
/opt/kata/share/kata-containers
```

Change the symbolic link.

```bash
sudo ln -sfn \
vmlinux-6.12.47-custom-cubic \
vmlinux.container
```

Verify:

```bash
readlink -f \
vmlinux.container
```

Expected:

```text
/opt/kata/share/kata-containers/vmlinux-6.12.47-custom-cubic
```

Restart containerd.

```bash
sudo systemctl restart \
containerd
```

Create the Kata container again.

```bash
sudo nerdctl run -d \
--name kata-test \
--runtime io.containerd.kata.v2 \
jjong2/all:latest \
sleep infinity
```

Verify the selected kernel.

```bash
sudo kata-runtime env \
| grep -A5 '\[Kernel\]'
```

Expected:

```text
Path = "/opt/kata/share/kata-containers/vmlinux-6.12.47-custom-cubic"
```

Verify CUBIC.

```bash
sudo nerdctl exec \
kata-test \
sysctl net.ipv4.tcp_congestion_control
```

Expected:

```text
net.ipv4.tcp_congestion_control = cubic
```

This configuration is:

```text
Pre-GSO = ON
CUBIC   = ON
```

---

# 27. Quick Baseline Kernel Switch

Use the following commands when switching to the CUBIC baseline.

```bash
sudo nerdctl rm -f \
kata-test \
2>/dev/null || true

cd \
/opt/kata/share/kata-containers

sudo ln -sfn \
vmlinux-6.12.47-202 \
vmlinux.container

sudo systemctl restart \
containerd

sudo nerdctl run -d \
--name kata-test \
--runtime io.containerd.kata.v2 \
jjong2/all:latest \
sleep infinity
```

Verify:

```bash
readlink -f \
/opt/kata/share/kata-containers/vmlinux.container

sudo kata-runtime env \
| grep -A5 '\[Kernel\]'

sudo nerdctl exec \
kata-test \
uname -r

sudo nerdctl exec \
kata-test \
sysctl net.ipv4.tcp_congestion_control
```

Expected:

```text
Kernel image = vmlinux-6.12.47-202
Kernel       = 6.12.47
CCA          = cubic
Pre-GSO      = OFF
```

---

# 28. Quick Pre-GSO Kernel Switch

Use the following commands when switching to the Pre-GSO guest kernel.

```bash
sudo nerdctl rm -f \
kata-test \
2>/dev/null || true

cd \
/opt/kata/share/kata-containers

sudo ln -sfn \
vmlinux-6.12.47-custom-cubic \
vmlinux.container

sudo systemctl restart \
containerd

sudo nerdctl run -d \
--name kata-test \
--runtime io.containerd.kata.v2 \
jjong2/all:latest \
sleep infinity
```

Verify:

```bash
readlink -f \
/opt/kata/share/kata-containers/vmlinux.container

sudo kata-runtime env \
| grep -A5 '\[Kernel\]'

sudo nerdctl exec \
kata-test \
uname -r

sudo nerdctl exec \
kata-test \
sysctl net.ipv4.tcp_congestion_control
```

Expected:

```text
Kernel image = vmlinux-6.12.47-custom-cubic
Kernel       = 6.12.47
CCA          = cubic
Pre-GSO      = ON
```

---

# 29. Optional Kernel-Switch Script

The following script allows the guest kernel to be switched with one command.

Create the script.

```bash
nano \
~/switch-kata-kernel.sh
```

Paste:

```bash
#!/bin/bash

set -e

KATA_DIR="/opt/kata/share/kata-containers"

BASELINE_KERNEL="vmlinux-6.12.47-202"
PREGSO_KERNEL="vmlinux-6.12.47-custom-cubic"

CONTAINER_NAME="kata-test"
CONTAINER_IMAGE="jjong2/all:latest"

if [ "$#" -ne 1 ]; then
    echo "Usage:"
    echo "  $0 baseline"
    echo "  $0 pregso"
    exit 1
fi

case "$1" in

    baseline)
        TARGET_KERNEL="$BASELINE_KERNEL"
        ;;

    pregso)
        TARGET_KERNEL="$PREGSO_KERNEL"
        ;;

    *)
        echo "Invalid option: $1"
        echo "Use 'baseline' or 'pregso'"
        exit 1
        ;;

esac

echo "========================================"
echo "Switching Kata guest kernel"
echo "Target: $TARGET_KERNEL"
echo "========================================"

sudo nerdctl rm -f \
"$CONTAINER_NAME" \
2>/dev/null || true

cd \
"$KATA_DIR"

sudo ln -sfn \
"$TARGET_KERNEL" \
vmlinux.container

echo
echo "[Kernel symlink]"

readlink -f \
vmlinux.container

echo
echo "[Restarting containerd]"

sudo systemctl restart \
containerd

echo
echo "[Creating Kata container]"

sudo nerdctl run -d \
--name "$CONTAINER_NAME" \
--runtime io.containerd.kata.v2 \
"$CONTAINER_IMAGE" \
sleep infinity

echo
echo "[Kata runtime kernel]"

sudo kata-runtime env \
| grep -A5 '\[Kernel\]'

echo
echo "[Guest kernel]"

sudo nerdctl exec \
"$CONTAINER_NAME" \
uname -r

echo
echo "[TCP congestion control]"

sudo nerdctl exec \
"$CONTAINER_NAME" \
sysctl net.ipv4.tcp_congestion_control

echo
echo "[Available congestion controls]"

sudo nerdctl exec \
"$CONTAINER_NAME" \
sysctl net.ipv4.tcp_available_congestion_control

echo
echo "========================================"
echo "Kernel switch complete"
echo "========================================"
```

Make it executable.

```bash
chmod +x \
~/switch-kata-kernel.sh
```

Switch to the baseline kernel:

```bash
~/switch-kata-kernel.sh \
baseline
```

Switch to the Pre-GSO kernel:

```bash
~/switch-kata-kernel.sh \
pregso
```

---

# 30. Experimental Kernel Configuration

The guest-kernel image controls Pre-GSO.

ACA is controlled separately through the host-side vCPU affinity.

| Configuration | Guest kernel                   | Pre-GSO | ACA | CCA   |
| ------------- | ------------------------------ | ------: | --: | ----- |
| Baseline      | `vmlinux-6.12.47-202`          |     OFF | OFF | CUBIC |
| ACA only      | `vmlinux-6.12.47-202`          |     OFF |  ON | CUBIC |
| Pre-GSO only  | `vmlinux-6.12.47-custom-cubic` |      ON | OFF | CUBIC |
| ACA + Pre-GSO | `vmlinux-6.12.47-custom-cubic` |      ON |  ON | CUBIC |

Thus, Pre-GSO and ACA can be independently enabled or disabled.

---

# 31. Important Notes

## 31.1 `uname -r` is not enough

Both kernels report:

```text
6.12.47
```

Therefore, do not use only:

```bash
uname -r
```

to determine whether the Pre-GSO kernel is active.

Always verify:

```bash
sudo kata-runtime env \
| grep -A5 '\[Kernel\]'
```

For the baseline:

```text
Path = "/opt/kata/share/kata-containers/vmlinux-6.12.47-202"
```

For Pre-GSO:

```text
Path = "/opt/kata/share/kata-containers/vmlinux-6.12.47-custom-cubic"
```

---

## 31.2 Recreate the Kata VM after changing the kernel

An already-running Kata VM continues using its original guest kernel.

The correct sequence is:

```text
Remove current Kata container
        ↓
Change vmlinux.container
        ↓
Restart containerd
        ↓
Create a new Kata container
        ↓
Verify the kernel path
        ↓
Verify CUBIC
```

---

## 31.3 Keep the baseline kernel unchanged

Do not overwrite:

```text
vmlinux-6.12.47-202
```

Store the modified kernel separately:

```text
vmlinux-6.12.47-custom-cubic
```

This makes it possible to repeatedly switch between the two environments without rebuilding the kernel.

---

## 31.4 Verify CUBIC every time the VM is recreated

**Command**

```bash
sudo nerdctl exec \
kata-test \
sysctl net.ipv4.tcp_congestion_control
```

Expected:

```text
net.ipv4.tcp_congestion_control = cubic
```

Available congestion-control algorithms:

```bash
sudo nerdctl exec \
kata-test \
sysctl net.ipv4.tcp_available_congestion_control
```

Expected:

```text
net.ipv4.tcp_available_congestion_control = reno bbr cubic
```

---

# 32. Final Verification Checklist

## Baseline CUBIC Kernel

```text
[ ] vmlinux.container -> vmlinux-6.12.47-202
[ ] kata-runtime env shows vmlinux-6.12.47-202
[ ] guest uname -r = 6.12.47
[ ] tcp_congestion_control = cubic
[ ] Pre-GSO = OFF
```

## Pre-GSO CUBIC Kernel

```text
[ ] vmlinux.container -> vmlinux-6.12.47-custom-cubic
[ ] kata-runtime env shows vmlinux-6.12.47-custom-cubic
[ ] guest uname -r = 6.12.47
[ ] tcp_congestion_control = cubic
[ ] Pre-GSO source modification is present
[ ] Pre-GSO = ON
```

---

# 33. Summary

The complete guest-kernel modification procedure is:

```text
Existing CUBIC baseline
vmlinux-6.12.47-202
        │
        │ reuse config-6.12.47-202
        ▼
Prepare Linux 6.12.47 source
        │
        ▼
kata-linux-6.12.47-173
        │
        │ modify Pre-GSO source
        ▼
Verify source + CUBIC
        │
        ▼
Build kernel
        │
        ▼
arch/arm64/boot/Image
        │
        ▼
vmlinux-6.12.47-custom-cubic
        │
        ▼
vmlinux.container symlink
        │
        ▼
Restart containerd
        │
        ▼
Recreate Kata VM
        │
        ▼
Verify kernel path
        │
        ▼
Verify CUBIC
```

After both kernels have been built, no additional compilation is required to move between them:

```text
Baseline CUBIC
vmlinux.container
        ↓
vmlinux-6.12.47-202

          ↕

Pre-GSO + CUBIC
vmlinux.container
        ↓
vmlinux-6.12.47-custom-cubic
```

This allows all revised experiments to use the same **CUBIC congestion-control configuration** while independently controlling whether the **Pre-GSO mechanism** is enabled.
