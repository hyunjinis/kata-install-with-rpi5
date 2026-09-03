# kata-install-with-rpi5

## Environment Setup
#### sudo apt install && sudo apt update && wget https://github.com/kata-containers/kata-containers/releases/download/3.24.0/kata-static-3.24.0-arm64.tar.zst && sudo tar -xvf kata-static-3.24.0-arm64.tar.zst -C / && rm kata-static-3.24.0-arm64.tar.zst && sudo ln -s /opt/kata/bin/kata-runtime /usr/local/bin && sudo ln -s /opt/kata/bin/containerd-shim-kata-v2 /usr/local/bin && sudo ln -s /opt/kata/bin/kata-collect-data.sh /usr/local/bin
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
0 upgraded, 0 newly installed, 0 to remove and 203 not upgraded.
Hit:1 https://prod-cdn.packages.k8s.io/repositories/isv:/kubernetes:/core:/stable:/v1.28/deb  InRelease
Hit:2 http://ports.ubuntu.com/ubuntu-ports noble InRelease
Get:3 http://ports.ubuntu.com/ubuntu-ports noble-backports InRelease [126 kB]
Get:4 http://ports.ubuntu.com/ubuntu-ports noble-security InRelease [126 kB]
Get:5 http://ports.ubuntu.com/ubuntu-ports noble-updates InRelease [126 kB]
Get:6 http://ports.ubuntu.com/ubuntu-ports noble-backports/main arm64 Components [3560 B]
Get:7 http://ports.ubuntu.com/ubuntu-ports noble-backports/universe arm64 Components [10.5 kB]
Get:8 http://ports.ubuntu.com/ubuntu-ports noble-backports/restricted arm64 Components [212 B]
Get:9 http://ports.ubuntu.com/ubuntu-ports noble-backports/multiverse arm64 Components [212 B]
Get:10 http://ports.ubuntu.com/ubuntu-ports noble-security/main arm64 Components [18.4 kB]
Get:11 http://ports.ubuntu.com/ubuntu-ports noble-security/main arm64 c-n-f Metadata [9672 B]
Get:12 http://ports.ubuntu.com/ubuntu-ports noble-security/universe arm64 Components [74.2 kB]
Get:13 http://ports.ubuntu.com/ubuntu-ports noble-security/universe arm64 c-n-f Metadata [20.0 kB]
Get:14 http://ports.ubuntu.com/ubuntu-ports noble-security/restricted arm64 Components [208 B]
Get:15 http://ports.ubuntu.com/ubuntu-ports noble-security/multiverse arm64 Components [208 B]
Get:16 http://ports.ubuntu.com/ubuntu-ports noble-updates/main arm64 Packages [1903 kB]
Get:17 http://ports.ubuntu.com/ubuntu-ports noble-updates/main arm64 Components [172 kB]
Get:18 http://ports.ubuntu.com/ubuntu-ports noble-updates/universe arm64 Packages [1520 kB]
Get:19 http://ports.ubuntu.com/ubuntu-ports noble-updates/universe arm64 Components [385 kB]
Get:20 http://ports.ubuntu.com/ubuntu-ports noble-updates/restricted arm64 Components [212 B]
Get:21 http://ports.ubuntu.com/ubuntu-ports noble-updates/multiverse arm64 Components [212 B]
Fetched 4373 kB in 6s (717 kB/s)
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
203 packages can be upgraded. Run 'apt list --upgradable' to see them.
--2026-02-27 17:42:54--  https://github.com/kata-containers/kata-containers/releases/download/3.24.0/kata-static-3.24.0-arm64.tar.zst
Resolving github.com (github.com)... 20.200.245.247
Connecting to github.com (github.com)|20.200.245.247|:443... connected.
HTTP request sent, awaiting response... 302 Found
Location: https://release-assets.githubusercontent.com/github-production-release-asset/113404957/2f5cb156-d666-4688-b09e-dd57598bb32d?sp=r&sv=2018-11-09&sr=b&spr=https&se=2026-02-27T09%3A20%3A14Z&rscd=attachment%3B+filename%3Dkata-static-3.24.0-arm64.tar.zst&rsct=application%2Foctet-stream&skoid=96c2d410-5711-43a1-aedd-ab1947aa7ab0&sktid=398a6654-997b-47e9-b12b-9515b896b4de&skt=2026-02-27T08%3A19%3A26Z&ske=2026-02-27T09%3A20%3A14Z&sks=b&skv=2018-11-09&sig=oQZAa9HweUTNe0nweip9H0LBm6VUEpbQW9%2BX2KYN8do%3D&jwt=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmVsZWFzZS1hc3NldHMuZ2l0aHVidXNlcmNvbnRlbnQuY29tIiwia2V5Ijoia2V5MSIsImV4cCI6MTc3MjE4NTM3NCwibmJmIjoxNzcyMTgxNzc0LCJwYXRoIjoicmVsZWFzZWFzc2V0cHJvZHVjdGlvbi5ibG9iLmNvcmUud2luZG93cy5uZXQifQ.kfQO6_37dhLGH74Z-lR9VIj7D1OMBKIC2G8RX4hwoI0&response-content-disposition=attachment%3B%20filename%3Dkata-static-3.24.0-arm64.tar.zst&response-content-type=application%2Foctet-stream [following]
--2026-02-27 17:42:54--  https://release-assets.githubusercontent.com/github-production-release-asset/113404957/2f5cb156-d666-4688-b09e-dd57598bb32d?sp=r&sv=2018-11-09&sr=b&spr=https&se=2026-02-27T09%3A20%3A14Z&rscd=attachment%3B+filename%3Dkata-static-3.24.0-arm64.tar.zst&rsct=application%2Foctet-stream&skoid=96c2d410-5711-43a1-aedd-ab1947aa7ab0&sktid=398a6654-997b-47e9-b12b-9515b896b4de&skt=2026-02-27T08%3A19%3A26Z&ske=2026-02-27T09%3A20%3A14Z&sks=b&skv=2018-11-09&sig=oQZAa9HweUTNe0nweip9H0LBm6VUEpbQW9%2BX2KYN8do%3D&jwt=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmVsZWFzZS1hc3NldHMuZ2l0aHVidXNlcmNvbnRlbnQuY29tIiwia2V5Ijoia2V5MSIsImV4cCI6MTc3MjE4NTM3NCwibmJmIjoxNzcyMTgxNzc0LCJwYXRoIjoicmVsZWFzZWFzc2V0cHJvZHVjdGlvbi5ibG9iLmNvcmUud2luZG93cy5uZXQifQ.kfQO6_37dhLGH74Z-lR9VIj7D1OMBKIC2G8RX4hwoI0&response-content-disposition=attachment%3B%20filename%3Dkata-static-3.24.0-arm64.tar.zst&response-content-type=application%2Foctet-stream
Resolving release-assets.githubusercontent.com (release-assets.githubusercontent.com)... 185.199.109.133, 185.199.111.133, 185.199.108.133, ...
Connecting to release-assets.githubusercontent.com (release-assets.githubusercontent.com)|185.199.109.133|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 476813228 (455M) [application/octet-stream]
Saving to: ‘kata-static-3.24.0-arm64.tar.zst’

kata-static-3.24.0- 100%[===================>] 454.72M  15.5MB/s    in 48s

2026-02-27 17:43:42 (9.55 MB/s) - ‘kata-static-3.24.0-arm64.tar.zst’ saved [476813228/476813228]

./
./opt/
./opt/kata/
./opt/kata/versions.yaml
./opt/kata/share/
./opt/kata/share/kata-containers/
./opt/kata/share/kata-containers/kata-ubuntu-noble-nvidia-gpu-580.95.05.initrd
./opt/kata/share/kata-containers/kata-alpine-3.22.initrd
./opt/kata/share/kata-containers/kata-containers.img
./opt/kata/share/kata-containers/vmlinux-confidential.container
./opt/kata/share/kata-containers/vmlinuz-6.12.47-173-dragonball-experimental
./opt/kata/share/kata-containers/kata-containers-initrd-nvidia-gpu.img
./opt/kata/share/kata-containers/kata-containers-nvidia-gpu.img
./opt/kata/share/kata-containers/kata-ubuntu-noble-nvidia-gpu-580.95.05.image
./opt/kata/share/kata-containers/vmlinux-6.15.0-rc1-916aeec68dd4500a1cdf4ebf214c5620955daf3f-173-confidential
./opt/kata/share/kata-containers/config-6.15.0-rc1-916aeec68dd4500a1cdf4ebf214c5620955daf3f-173-confidential
./opt/kata/share/kata-containers/vmlinuz.container
./opt/kata/share/kata-containers/vmlinux-nvidia-gpu.container
./opt/kata/share/kata-containers/config-6.12.47-173-dragonball-experimental
./opt/kata/share/kata-containers/vmlinuz-nvidia-gpu.container
./opt/kata/share/kata-containers/config-6.12.47-173
./opt/kata/share/kata-containers/config-6.12.47-173-nvidia-gpu
./opt/kata/share/kata-containers/vmlinuz-6.12.47-173
./opt/kata/share/kata-containers/kata-ubuntu-noble.image
./opt/kata/share/kata-containers/vmlinux-dragonball-experimental.container
./opt/kata/share/kata-containers/kata-containers-initrd.img
./opt/kata/share/kata-containers/vmlinuz-6.12.47-173-nvidia-gpu
./opt/kata/share/kata-containers/vmlinux.container
./opt/kata/share/kata-containers/vmlinux-6.12.47-173
./opt/kata/share/kata-containers/vmlinuz-confidential.container
./opt/kata/share/kata-containers/vmlinux-6.12.47-173-nvidia-gpu
./opt/kata/share/kata-containers/vmlinux-6.12.47-173-dragonball-experimental
./opt/kata/share/kata-containers/vmlinuz-6.15.0-rc1-916aeec68dd4500a1cdf4ebf214c5620955daf3f-173-confidential
./opt/kata/share/kata-containers/vmlinuz-dragonball-experimental.container
./opt/kata/share/kata-qemu/
./opt/kata/share/kata-qemu/qemu/
./opt/kata/share/kata-qemu/qemu/edk2-aarch64-code.fd
./opt/kata/share/kata-qemu/qemu/multiboot_dma.bin
./opt/kata/share/kata-qemu/qemu/slof.bin
./opt/kata/share/kata-qemu/qemu/bios-microvm.bin
./opt/kata/share/kata-qemu/qemu/npcm8xx_bootrom.bin
./opt/kata/share/kata-qemu/qemu/qemu-nsis.bmp
./opt/kata/share/kata-qemu/qemu/edk2-i386-vars.fd
./opt/kata/share/kata-qemu/qemu/firmware/
./opt/kata/share/kata-qemu/qemu/firmware/60-edk2-loongarch64.json
./opt/kata/share/kata-qemu/qemu/firmware/60-edk2-riscv64.json
./opt/kata/share/kata-qemu/qemu/firmware/60-edk2-x86_64.json
./opt/kata/share/kata-qemu/qemu/firmware/50-edk2-i386-secure.json
./opt/kata/share/kata-qemu/qemu/firmware/60-edk2-i386.json
./opt/kata/share/kata-qemu/qemu/firmware/60-edk2-aarch64.json
./opt/kata/share/kata-qemu/qemu/firmware/60-edk2-arm.json
./opt/kata/share/kata-qemu/qemu/firmware/50-edk2-x86_64-secure.json
./opt/kata/share/kata-qemu/qemu/edk2-i386-secure-code.fd
./opt/kata/share/kata-qemu/qemu/pnv-pnor.bin
./opt/kata/share/kata-qemu/qemu/linuxboot.bin
./opt/kata/share/kata-qemu/qemu/ast27x0_bootrom.bin
./opt/kata/share/kata-qemu/qemu/edk2-licenses.txt
./opt/kata/share/kata-qemu/qemu/kvmvapic.bin
./opt/kata/share/kata-qemu/qemu/edk2-loongarch64-vars.fd
./opt/kata/share/kata-qemu/qemu/edk2-arm-vars.fd
./opt/kata/share/kata-qemu/qemu/s390-ccw.img
./opt/kata/share/kata-qemu/qemu/bios.bin
./opt/kata/share/kata-qemu/qemu/edk2-riscv-vars.fd
./opt/kata/share/kata-qemu/qemu/edk2-loongarch64-code.fd
./opt/kata/share/kata-qemu/qemu/vof-nvram.bin
./opt/kata/share/kata-qemu/qemu/hppa-firmware64.img
./opt/kata/share/kata-qemu/qemu/edk2-arm-code.fd
./opt/kata/share/kata-qemu/qemu/efi-virtio.rom
./opt/kata/share/kata-qemu/qemu/pvh.bin
./opt/kata/share/kata-qemu/qemu/edk2-x86_64-secure-code.fd
./opt/kata/share/kata-qemu/qemu/bios-256k.bin
./opt/kata/share/kata-qemu/qemu/vof.bin
./opt/kata/share/kata-qemu/qemu/qboot.rom
./opt/kata/share/kata-qemu/qemu/dtb/
./opt/kata/share/kata-qemu/qemu/edk2-x86_64-code.fd
./opt/kata/share/kata-qemu/qemu/hppa-firmware.img
./opt/kata/share/kata-qemu/qemu/edk2-riscv-code.fd
./opt/kata/share/kata-qemu/qemu/edk2-i386-code.fd
./opt/kata/share/kata-qemu/qemu/linuxboot_dma.bin
./opt/kata/share/bash-completion/
./opt/kata/share/bash-completion/completions/
./opt/kata/share/bash-completion/completions/kata-runtime
./opt/kata/share/aavmf/
./opt/kata/share/aavmf/AAVMF_CODE.fd
./opt/kata/share/aavmf/AAVMF_VARS.fd
./opt/kata/share/defaults/
./opt/kata/share/defaults/kata-containers/
./opt/kata/share/defaults/kata-containers/configuration-qemu-nvidia-gpu-snp.toml
./opt/kata/share/defaults/kata-containers/configuration-qemu-nvidia-gpu-tdx.toml
./opt/kata/share/defaults/kata-containers/configuration-qemu-cca.toml
./opt/kata/share/defaults/kata-containers/configuration-qemu-nvidia-gpu.toml
./opt/kata/share/defaults/kata-containers/configuration-qemu-tdx.toml
./opt/kata/share/defaults/kata-containers/runtime-rs/
./opt/kata/share/defaults/kata-containers/runtime-rs/configuration-qemu-se-runtime-rs.toml
./opt/kata/share/defaults/kata-containers/runtime-rs/configuration-dragonball.toml
./opt/kata/share/defaults/kata-containers/runtime-rs/configuration-qemu-runtime-rs.toml
./opt/kata/share/defaults/kata-containers/runtime-rs/configuration-qemu-coco-dev-runtime-rs.toml
./opt/kata/share/defaults/kata-containers/runtime-rs/configuration-rs-fc.toml
./opt/kata/share/defaults/kata-containers/runtime-rs/configuration.toml
./opt/kata/share/defaults/kata-containers/configuration-remote.toml
./opt/kata/share/defaults/kata-containers/configuration-clh.toml
./opt/kata/share/defaults/kata-containers/configuration-qemu-snp.toml
./opt/kata/share/defaults/kata-containers/configuration.toml
./opt/kata/share/defaults/kata-containers/configuration-qemu-coco-dev.toml
./opt/kata/share/defaults/kata-containers/configuration-qemu.toml
./opt/kata/share/defaults/kata-containers/configuration-qemu-se.toml
./opt/kata/share/defaults/kata-containers/configuration-stratovirt.toml
./opt/kata/share/defaults/kata-containers/configuration-fc.toml
./opt/kata/libexec/
./opt/kata/libexec/virtiofsd
./opt/kata/libexec/nydusd
./opt/kata/runtime-rs/
./opt/kata/runtime-rs/bin/
./opt/kata/runtime-rs/bin/containerd-shim-kata-v2
./opt/kata/VERSION
./opt/kata/include/
./opt/kata/include/fdt.h
./opt/kata/include/libfdt_env.h
./opt/kata/include/libfdt.h
./opt/kata/bin/
./opt/kata/bin/firecracker
./opt/kata/bin/kata-collect-data.sh
./opt/kata/bin/jailer
./opt/kata/bin/containerd-shim-kata-v2
./opt/kata/bin/cloud-hypervisor
./opt/kata/bin/qemu-system-aarch64
./opt/kata/bin/kata-monitor
./opt/kata/bin/kata-runtime
./opt/kata/lib/
./opt/kata/lib/kata-qemu/
./opt/kata/lib/kata-qemu/libfdt.a
./opt/kata/lib/kata-qemu/pkgconfig/
./opt/kata/lib/kata-qemu/pkgconfig/libfdt.pc

#### sudo modprobe vhost
#### sudo modprobe vhost_net
#### sudo modprobe vhost_vsock

#### lsmod | grep -E 'vhost|vsock|tap'
vhost_vsock            24576  0
vmw_vsock_virtio_transport_common    53248  1 vhost_vsock
vsock                  61440  2 vmw_vsock_virtio_transport_common,vhost_vsock
vhost_net              32768  0
tun                    61440  1 vhost_net
tap                    36864  1 vhost_net
vhost                  69632  2 vhost_vsock,vhost_net
vhost_iotlb            16384  1 vhost

#### kata-runtime --version
kata-runtime  : 3.24.0
   commit   : c7d0c270ee7dfaa6d978e6e07b99dabdaf2b9fda
   OCI specs: 1.2.1
   
#### sudo kata-runtime check
WARN[0000] Not running network checks as super user      arch=arm64 name=kata-runtime pid=1800336 source=runtime
System is capable of running Kata Containers
System can currently create Kata Containers

#### sudo apt install -y flex bison libelf-dev libncurses-dev

#### wget https://go.dev/dl/go1.26.0.linux-arm64.tar.gz

#### sudo rm -rf /usr/local/go
#### sudo tar -C /usr/local -xzf go1.26.0.linux-arm64.tar.gz

#### echo 'export PATH=$PATH:/usr/local/go/bin' >> ~/.bashrc
#### source ~/.bashrc

#### go version
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
flex is already the newest version (2.6.4-8.2build1).
bison is already the newest version (2:3.8.2+dfsg-1build2).
The following additional packages will be installed:
  libncurses6 libncursesw6 libtinfo6 libzstd-dev ncurses-base ncurses-bin ncurses-term zlib1g zlib1g-dev
Suggested packages:
  ncurses-doc
The following NEW packages will be installed:
  libelf-dev libzstd-dev zlib1g-dev
The following packages will be upgraded:
  libncurses-dev libncurses6 libncursesw6 libtinfo6 ncurses-base ncurses-bin ncurses-term zlib1g
8 upgraded, 3 newly installed, 0 to remove and 544 not upgraded.
Need to get 2603 kB of archives.
After this operation, 2930 kB of additional disk space will be used.
Get:1 http://ports.ubuntu.com/ubuntu-ports noble-updates/main arm64 ncurses-bin arm64 6.4+20240113-1ubuntu2.2 [186 kB]
Get:2 http://ports.ubuntu.com/ubuntu-ports noble-updates/main arm64 ncurses-base all 6.4+20240113-1ubuntu2.2 [25.8 kB]
Get:3 http://ports.ubuntu.com/ubuntu-ports noble-updates/main arm64 ncurses-term all 6.4+20240113-1ubuntu2.2 [275 kB]
Get:4 http://ports.ubuntu.com/ubuntu-ports noble-updates/main arm64 libncurses-dev arm64 6.4+20240113-1ubuntu2.2 [385 kB]
Get:5 http://ports.ubuntu.com/ubuntu-ports noble-updates/main arm64 libncurses6 arm64 6.4+20240113-1ubuntu2.2 [110 kB]
Get:6 http://ports.ubuntu.com/ubuntu-ports noble-updates/main arm64 libncursesw6 arm64 6.4+20240113-1ubuntu2.2 [146 kB]
Get:7 http://ports.ubuntu.com/ubuntu-ports noble-updates/main arm64 libtinfo6 arm64 6.4+20240113-1ubuntu2.2 [105 kB]
Get:8 http://ports.ubuntu.com/ubuntu-ports noble-updates/main arm64 zlib1g arm64 1:1.3.dfsg-3.1ubuntu2.2 [61.9 kB]
Get:9 http://ports.ubuntu.com/ubuntu-ports noble-updates/main arm64 zlib1g-dev arm64 1:1.3.dfsg-3.1ubuntu2.2 [894 kB]
Get:10 http://ports.ubuntu.com/ubuntu-ports noble-updates/main arm64 libzstd-dev arm64 1.5.5+dfsg2-2build1.1 [344 kB]
Get:11 http://ports.ubuntu.com/ubuntu-ports noble-updates/main arm64 libelf-dev arm64 0.190-1.1ubuntu0.1 [72.2 kB]
Fetched 2603 kB in 3s (989 kB/s)     
(Reading database ... 155942 files and directories currently installed.)
Preparing to unpack .../ncurses-bin_6.4+20240113-1ubuntu2.2_arm64.deb ...
Unpacking ncurses-bin (6.4+20240113-1ubuntu2.2) over (6.4+20240113-1ubuntu2) ...
Setting up ncurses-bin (6.4+20240113-1ubuntu2.2) ...
(Reading database ... 155942 files and directories currently installed.)
Preparing to unpack .../ncurses-base_6.4+20240113-1ubuntu2.2_all.deb ...
Unpacking ncurses-base (6.4+20240113-1ubuntu2.2) over (6.4+20240113-1ubuntu2) ...
Setting up ncurses-base (6.4+20240113-1ubuntu2.2) ...
(Reading database ... 155942 files and directories currently installed.)
Preparing to unpack .../ncurses-term_6.4+20240113-1ubuntu2.2_all.deb ...
Unpacking ncurses-term (6.4+20240113-1ubuntu2.2) over (6.4+20240113-1ubuntu2) ...
Preparing to unpack .../libncurses-dev_6.4+20240113-1ubuntu2.2_arm64.deb ...
Unpacking libncurses-dev:arm64 (6.4+20240113-1ubuntu2.2) over (6.4+20240113-1ubuntu2) ...
Preparing to unpack .../libncurses6_6.4+20240113-1ubuntu2.2_arm64.deb ...
Unpacking libncurses6:arm64 (6.4+20240113-1ubuntu2.2) over (6.4+20240113-1ubuntu2) ...
Preparing to unpack .../libncursesw6_6.4+20240113-1ubuntu2.2_arm64.deb ...
Unpacking libncursesw6:arm64 (6.4+20240113-1ubuntu2.2) over (6.4+20240113-1ubuntu2) ...
Preparing to unpack .../libtinfo6_6.4+20240113-1ubuntu2.2_arm64.deb ...
Unpacking libtinfo6:arm64 (6.4+20240113-1ubuntu2.2) over (6.4+20240113-1ubuntu2) ...
Setting up libtinfo6:arm64 (6.4+20240113-1ubuntu2.2) ...
(Reading database ... 155942 files and directories currently installed.)
Preparing to unpack .../zlib1g_1%3a1.3.dfsg-3.1ubuntu2.2_arm64.deb ...
Unpacking zlib1g:arm64 (1:1.3.dfsg-3.1ubuntu2.2) over (1:1.3.dfsg-3.1ubuntu2) ...
Setting up zlib1g:arm64 (1:1.3.dfsg-3.1ubuntu2.2) ...
Selecting previously unselected package zlib1g-dev:arm64.
(Reading database ... 155942 files and directories currently installed.)
Preparing to unpack .../zlib1g-dev_1%3a1.3.dfsg-3.1ubuntu2.2_arm64.deb ...
Unpacking zlib1g-dev:arm64 (1:1.3.dfsg-3.1ubuntu2.2) ...
Selecting previously unselected package libzstd-dev:arm64.
Preparing to unpack .../libzstd-dev_1.5.5+dfsg2-2build1.1_arm64.deb ...
Unpacking libzstd-dev:arm64 (1.5.5+dfsg2-2build1.1) ...
Selecting previously unselected package libelf-dev:arm64.
Preparing to unpack .../libelf-dev_0.190-1.1ubuntu0.1_arm64.deb ...
Unpacking libelf-dev:arm64 (0.190-1.1ubuntu0.1) ...
Setting up libzstd-dev:arm64 (1.5.5+dfsg2-2build1.1) ...
Setting up libncurses6:arm64 (6.4+20240113-1ubuntu2.2) ...
Setting up libncursesw6:arm64 (6.4+20240113-1ubuntu2.2) ...
Setting up zlib1g-dev:arm64 (1:1.3.dfsg-3.1ubuntu2.2) ...
Setting up ncurses-term (6.4+20240113-1ubuntu2.2) ...
Setting up libncurses-dev:arm64 (6.4+20240113-1ubuntu2.2) ...
Setting up libelf-dev:arm64 (0.190-1.1ubuntu0.1) ...
Processing triggers for man-db (2.12.0-4build2) ...
Processing triggers for libc-bin (2.39-0ubuntu8.7) ...
--2026-09-03 14:37:49--  https://go.dev/dl/go1.26.0.linux-arm64.tar.gz
Resolving go.dev (go.dev)... 216.239.34.21, 216.239.32.21, 216.239.36.21, ...
Connecting to go.dev (go.dev)|216.239.34.21|:443... connected.
HTTP request sent, awaiting response... 302 Found
Location: https://dl.google.com/go/go1.26.0.linux-arm64.tar.gz [following]
--2026-09-03 14:37:49--  https://dl.google.com/go/go1.26.0.linux-arm64.tar.gz
Resolving dl.google.com (dl.google.com)... 172.217.211.190, 172.217.211.136, 172.217.211.91, ...
Connecting to dl.google.com (dl.google.com)|172.217.211.190|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 63655921 (61M) [application/x-gzip]
Saving to: ‘go1.26.0.linux-arm64.tar.gz’

go1.26.0.linux-arm64.tar.gz                 100%[=========================================================================================>]  60.71M  41.3MB/s    in 1.5s    

2026-09-03 14:37:51 (41.3 MB/s) - ‘go1.26.0.linux-arm64.tar.gz’ saved [63655921/63655921]

go version go1.22.2 linux/arm64

#### sudo tar -C /usr/local -xzf go1.26.0.linux-arm64.tar.gz && \
#### echo 'export PATH=$PATH:/usr/local/go/bin' >> ~/.bashrc && \
#### source ~/.bashrc && \
#### curl https://sh.rustup.rs -sSf | sh -s -- -y && \
#### source "$HOME/.cargo/env" && \
#### go version && \
#### rustc --version
info: downloading installer
info: profile set to default
info: default host tuple is aarch64-unknown-linux-gnu
info: syncing channel updates for stable-aarch64-unknown-linux-gnu
info: latest update on 2026-08-20 for version 1.98.0 (88d9e12ae 2026-08-18)
info: downloading 6 components
        cargo installed                       10.60 MiB                                                                                                                              clippy installed                        3.74 MiB                                                                                                                           rust-docs installed                       22.97 MiB                                                                                                                            rust-std installed                       29.34 MiB                                                                                                                               rustc installed                       63.34 MiB                                                                                                                             rustfmt installed                        2.19 MiB                                                                                                                       info: default toolchain set to stable-aarch64-unknown-linux-gnu

  stable-aarch64-unknown-linux-gnu installed - rustc 1.98.0 (88d9e12ae 2026-08-18)


Rust is installed now. Great!

To get started you may need to restart your current shell.
This would reload your PATH environment variable to include
Cargo's bin directory ($HOME/.cargo/bin).

To configure your current shell, you need to source the
corresponding env file under $HOME/.cargo.

Consider running the right command for your shell (note the leading DOT):
. "$HOME/.cargo/env" # For sh/ash/dash/pdksh/bash
cargo:rerun-if-env-changed=CC_aarch64-unknown-linux-gnu
CC_aarch64-unknown-linux-gnu = None
cargo:rerun-if-env-changed=CC_aarch64_unknown_linux_gnu
CC_aarch64_unknown_linux_gnu = None
cargo:rerun-if-env-changed=HOST_CC
HOST_CC = None
cargo:rerun-if-env-changed=CC
CC = None
cargo:rerun-if-env-changed=CC_ENABLE_DEBUG_OUTPUT
cargo:rerun-if-env-changed=CRATE_CC_NO_DEFAULTS
CRATE_CC_NO_DEFAULTS = None
cargo:rerun-if-env-changed=CFLAGS
CFLAGS = None
cargo:rerun-if-env-changed=HOST_CFLAGS
HOST_CFLAGS = None
cargo:rerun-if-env-changed=CFLAGS_aarch64_unknown_linux_gnu
CFLAGS_aarch64_unknown_linux_gnu = None
cargo:rerun-if-env-changed=CFLAGS_aarch64-unknown-linux-gnu
CFLAGS_aarch64-unknown-linux-gnu = None
go version go1.22.2 linux/arm64
rustc 1.98.0 (88d9e12ae 2026-08-18)

#### go install github.com/mikefarah/yq/v4@v4.52.4 && echo 'export PATH=$PATH:$HOME/go/bin' >> ~/.bashrc && source ~/.bashrc && sudo cp $HOME/go/bin/yq /usr/local/bin/ && yq --version && git clone https://github.com/kata-containers/kata-containers.git ~/kata-containers
go: downloading github.com/mikefarah/yq/v4 v4.52.4
go: github.com/mikefarah/yq/v4@v4.52.4 requires go >= 1.24.0; switching to go1.26.8
go: downloading go1.26.8 (linux/arm64)
go: downloading github.com/spf13/cobra v1.10.2
go: downloading github.com/spf13/pflag v1.0.10
go: downloading gopkg.in/op/go-logging.v1 v1.0.0-20160211212156-b2cb9fa56473
go: downloading github.com/a8m/envsubst v1.4.3
go: downloading github.com/alecthomas/participle/v2 v2.1.4
go: downloading github.com/dimchansky/utfbom v1.1.1
go: downloading github.com/elliotchance/orderedmap v1.8.0
go: downloading github.com/fatih/color v1.18.0
go: downloading github.com/go-ini/ini v1.67.0
go: downloading github.com/goccy/go-json v0.10.5
go: downloading github.com/goccy/go-yaml v1.19.2
go: downloading github.com/hashicorp/hcl/v2 v2.24.0
go: downloading github.com/jinzhu/copier v0.4.0
go: downloading github.com/magiconair/properties v1.8.10
go: downloading github.com/pelletier/go-toml/v2 v2.2.4
go: downloading github.com/zclconf/go-cty v1.17.0
go: downloading github.com/yuin/gopher-lua v1.1.1
go: downloading go.yaml.in/yaml/v4 v4.0.0-rc.3
go: downloading golang.org/x/net v0.50.0
go: downloading golang.org/x/text v0.34.0
go: downloading github.com/mattn/go-colorable v0.1.14
go: downloading github.com/mattn/go-isatty v0.0.20
go: downloading github.com/agext/levenshtein v1.2.1
go: downloading github.com/apparentlymart/go-textseg/v15 v15.0.0
go: downloading github.com/mitchellh/go-wordwrap v1.0.1
go: downloading github.com/google/go-cmp v0.6.0
go: downloading golang.org/x/sys v0.41.0
go: github.com/mikefarah/yq/v4@v4.52.4 requires go >= 1.24.0; switching to go1.26.8
yq (https://github.com/mikefarah/yq/) version v4.52.4
Cloning into '/home/rpi3/kata-containers'...
remote: Enumerating objects: 175917, done.
remote: Counting objects: 100% (1675/1675), done.
remote: Compressing objects: 100% (764/764), done.
remote: Total 175917 (delta 1216), reused 911 (delta 911), pack-reused 174242 (from 3)
Receiving objects: 100% (175917/175917), 100.01 MiB | 24.68 MiB/s, done.
Resolving deltas: 100% (121156/121156), done.

#### cd kata-containers/tools/packaging/kernel
#### ~/kata-containers/tools/packaging/kernel# ./build-kernel.sh -a aarch64 -v 6.12.47 -f -d setup
Line 623: getopts a:b:c:dD:eEfg:hH:k:mp:r:st:u:v:x opt
 Line 695: shift 6
 Line 697: subcmd=setup
 Line 699: '[' -z setup ']'
 Line 701: [[ '' == \e\x\p\e\r\i\m\e\n\t\a\l ]]
 Line 712: '[' -z 6.12.47 ']'
 Line 737: kernel_version=6.12.47
 Line 739: '[' -z '' ']'
  Line 740: get_config_version
  Line 421: get_config_and_patches
  Line 415: '[' -z '' ']'
  Line 416: patches_path=/root/kata-containers/tools/packaging/kernel/patches
  Line 422: config_version_file=/root/kata-containers/tools/packaging/kernel/patches/../kata_config_version
  Line 423: '[' -f /root/kata-containers/tools/packaging/kernel/patches/../kata_config_version ']'
  Line 424: cat /root/kata-containers/tools/packaging/kernel/patches/../kata_config_version
 Line 740: config_version=182
 Line 741: [[ '' != '' ]]
 Line 744: kernel_path=/root/kata-containers/tools/packaging/kernel/kata-linux-6.12.47-182
 Line 746: info 'Config version: 182'
 Line 52: echo 'INFO: Config version: 182'
INFO: Config version: 182
 Line 749: info 'Kernel version: 6.12.47'
 Line 52: echo 'INFO: Kernel version: 6.12.47'
INFO: Kernel version: 6.12.47
  Line 751: uname -m
 Line 751: '[' aarch64 '!=' '' -a aarch64 '!=' aarch64 ']'
 Line 753: case "${subcmd}" in
 Line 764: setup_kernel /root/kata-containers/tools/packaging/kernel/kata-linux-6.12.47-182
 Line 431: local kernel_path=/root/kata-containers/tools/packaging/kernel/kata-linux-6.12.47-182
 Line 432: '[' -n /root/kata-containers/tools/packaging/kernel/kata-linux-6.12.47-182 ']'
 Line 434: [[ true == \t\r\u\e ]]
 Line 434: [[ -d /root/kata-containers/tools/packaging/kernel/kata-linux-6.12.47-182 ]]
 Line 439: '[' -d /root/kata-containers/tools/packaging/kernel/kata-linux-6.12.47-182 ']'
 Line 447: info 'kernel path does not exist, will download kernel'
 Line 52: echo 'INFO: kernel path does not exist, will download kernel'
INFO: kernel path does not exist, will download kernel
 Line 448: download_kernel=true
 Line 449: '[' -n 6.12.47 ']'
 Line 451: [[ true == \t\r\u\e ]]
 Line 452: '[' -z '' ']'
 Line 453: get_kernel 6.12.47 /root/kata-containers/tools/packaging/kernel/kata-linux-6.12.47-182
 Line 158: local version=6.12.47
 Line 160: local kernel_path=/root/kata-containers/tools/packaging/kernel/kata-linux-6.12.47-182
 Line 161: '[' -n /root/kata-containers/tools/packaging/kernel/kata-linux-6.12.47-182 ']'
 Line 162: '[' '!' -d /root/kata-containers/tools/packaging/kernel/kata-linux-6.12.47-182 ']'
 Line 165: version=6.12.47
  Line 167: echo 6.12.47
  Line 167: cut -d. -f1
 Line 167: local major_version=6
  Line 168: echo 6.12.47
  Line 168: grep -oE '\-rc[0-9]+$'
 Line 168: local rc=
 Line 170: local tar_suffix=tar.xz
 Line 171: '[' -n '' ']'
 Line 174: kernel_tarball=linux-6.12.47.tar.xz
 Line 176: '[' -z '' ']'
 Line 177: [[ -f linux-6.12.47.tar.xz.sha256 ]]
 Line 181: shasum_url=https://cdn.kernel.org/pub/linux/kernel/v6.x/sha256sums.asc
 Line 182: info 'Download kernel checksum file: sha256sums.asc from https://cdn.kernel.org/pub/linux/kernel/v6.x/sha256sums.asc'
 Line 52: echo 'INFO: Download kernel checksum file: sha256sums.asc from https://cdn.kernel.org/pub/linux/kernel/v6.x/sha256sums.asc'
INFO: Download kernel checksum file: sha256sums.asc from https://cdn.kernel.org/pub/linux/kernel/v6.x/sha256sums.asc
 Line 183: curl --fail -OL https://cdn.kernel.org/pub/linux/kernel/v6.x/sha256sums.asc
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100  198k  100  198k    0     0   115k      0  0:00:01  0:00:01 --:--:--  115k
 Line 184: grep -F linux-6.12.47.tar.xz sha256sums.asc
 Line 185: info 'sha256sums.asc is valid, linux-6.12.47.tar.xz.sha256 generated'
 Line 52: echo 'INFO: sha256sums.asc is valid, linux-6.12.47.tar.xz.sha256 generated'
INFO: sha256sums.asc is valid, linux-6.12.47.tar.xz.sha256 generated
 Line 194: '[' -f linux-6.12.47.tar.xz ']'
 Line 200: '[' '!' -f linux-6.12.47.tar.xz ']'
 Line 201: kernel_tarball_url=https://www.kernel.org/pub/linux/kernel/v6.x/linux-6.12.47.tar.xz
 Line 202: '[' -n '' ']'
 Line 205: info 'Download kernel version 6.12.47'
 Line 52: echo 'INFO: Download kernel version 6.12.47'
INFO: Download kernel version 6.12.47
 Line 206: info 'Download kernel from: https://www.kernel.org/pub/linux/kernel/v6.x/linux-6.12.47.tar.xz'
 Line 52: echo 'INFO: Download kernel from: https://www.kernel.org/pub/linux/kernel/v6.x/linux-6.12.47.tar.xz'
INFO: Download kernel from: https://www.kernel.org/pub/linux/kernel/v6.x/linux-6.12.47.tar.xz
 Line 207: curl --fail -OL https://www.kernel.org/pub/linux/kernel/v6.x/linux-6.12.47.tar.xz
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100  141M  100  141M    0     0  61.5M      0  0:00:02  0:00:02 --:--:-- 61.5M
 Line 212: '[' -z '' ']'
 Line 213: sha256sum -c linux-6.12.47.tar.xz.sha256
linux-6.12.47.tar.xz: OK
 Line 216: tar xf linux-6.12.47.tar.xz
 Line 218: mv linux-6.12.47 /root/kata-containers/tools/packaging/kernel/kata-linux-6.12.47-182
 Line 459: '[' -n /root/kata-containers/tools/packaging/kernel/kata-linux-6.12.47-182 ']'
 Line 462: get_config_and_patches
 Line 415: '[' -z '' ']'
 Line 416: patches_path=/root/kata-containers/tools/packaging/kernel/patches
 Line 464: '[' -d /root/kata-containers/tools/packaging/kernel/patches ']'
 Line 466: local major_kernel
  Line 467: get_major_kernel_version 6.12.47
  Line 222: local version=6.12.47
  Line 223: '[' -n 6.12.47 ']'
   Line 224: echo 6.12.47
   Line 224: cut -d. -f1
  Line 224: major_version=6
   Line 225: echo 6.12.47
   Line 225: cut -d. -f2
  Line 225: minor_version=12
  Line 226: echo 6.12
 Line 467: major_kernel=6.12
 Line 468: local patches_dir_for_version=/root/kata-containers/tools/packaging/kernel/patches/6.12.x
 Line 469: local build_type_patches_dir=/root/kata-containers/tools/packaging/kernel/patches/6.12.x/
 Line 471: '[' -n aarch64 ']'
  Line 472: arch_to_kernel aarch64
  Line 125: local -r arch=aarch64
  Line 127: case "$arch" in
  Line 128: echo arm64
 Line 472: arch_target=arm64
 Line 474: cd /root/kata-containers/tools/packaging/kernel/kata-linux-6.12.47-182
 Line 477: /root/kata-containers/tools/packaging/kernel/../scripts/apply_patches.sh /root/kata-containers/tools/packaging/kernel/patches/6.12.x
INFO: Apply patches from /root/kata-containers/tools/packaging/kernel/patches/6.12.x
INFO: Found 0 patches
 Line 480: '[' '' '!=' '' ']'
 Line 485: '[' -n '' ']'
 Line 485: hypervisor_target=kvm
 Line 486: '[' -n '' ']'
  Line 486: get_default_kernel_config 6.12.47 kvm arm64 /root/kata-containers/tools/packaging/kernel/kata-linux-6.12.47-182
  Line 392: local version=6.12.47
  Line 394: local hypervisor=kvm
  Line 395: local kernel_arch=arm64
  Line 396: local kernel_path=/root/kata-containers/tools/packaging/kernel/kata-linux-6.12.47-182
  Line 398: '[' -n 6.12.47 ']'
  Line 399: '[' -n kvm ']'
  Line 400: '[' -n arm64 ']'
  Line 402: archfragdir=/root/kata-containers/tools/packaging/kernel/configs/fragments/arm64
  Line 403: '[' -d /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64 ']'
   Line 404: get_kernel_frag_path /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64 /root/kata-containers/tools/packaging/kernel/kata-linux-6.12.47-182 arm64
   Line 235: local arch_path=/root/kata-containers/tools/packaging/kernel/configs/fragments/arm64
   Line 236: local common_path=/root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common
   Line 237: local gpu_path=/root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../gpu
   Line 238: local dpu_path=/root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../dpu
   Line 240: local kernel_path=/root/kata-containers/tools/packaging/kernel/kata-linux-6.12.47-182
   Line 241: local arch=arm64
   Line 242: local cmdpath=/root/kata-containers/tools/packaging/kernel/kata-linux-6.12.47-182/scripts/kconfig/merge_config.sh
   Line 243: local config_path=/root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/.config
    Line 245: ls /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/acpi.conf /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/base.conf /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/crypto.conf /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/dt.conf /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/erratum.conf /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/network.conf /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/numa.conf /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/pci.conf /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/ptp.conf /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/rtc.conf /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/serial.conf /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/virtio.conf
   Line 245: local 'arch_configs=/root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/acpi.conf
/root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/base.conf
/root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/crypto.conf
/root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/dt.conf
/root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/erratum.conf
/root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/network.conf
/root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/numa.conf
/root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/pci.conf
/root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/ptp.conf
/root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/rtc.conf
/root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/serial.conf
/root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/virtio.conf'
   Line 247: local 'exclude_tags=-e !arm64'
   Line 250: [[ '' != '' ]]
    Line 254: grep -e '!arm64' /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/9p.conf /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/acpi.conf /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/base.conf /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/cgroup.conf /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/cpu.conf /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/crypto.conf /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/dax.conf /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/debug.conf /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/elf.conf /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/fs.conf /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/hotplug.conf /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/huge.conf /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/lsm.conf /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/mem_agent.conf /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/mmio.conf /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/mmu.conf /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/namespaces.conf /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/netfilter.conf /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/network.conf /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/pmem.conf /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/seccomp.conf /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/security.conf /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/serial.conf /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/vfio.conf /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/virtio-extras.conf /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/virtio.conf -L
   Line 254: local 'common_configs=/root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/9p.conf
/root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/acpi.conf
/root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/base.conf
/root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/cgroup.conf
/root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/cpu.conf
/root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/crypto.conf
/root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/dax.conf
/root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/debug.conf
/root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/elf.conf
/root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/fs.conf
/root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/hotplug.conf
/root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/huge.conf
/root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/lsm.conf
/root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/mem_agent.conf
/root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/mmio.conf
/root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/mmu.conf
/root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/namespaces.conf
/root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/netfilter.conf
/root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/network.conf
/root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/pmem.conf
/root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/seccomp.conf
/root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/security.conf
/root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/serial.conf
/root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/vfio.conf
/root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/virtio-extras.conf
/root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/virtio.conf'
   Line 256: local extra_configs=
   Line 257: '[' '' '!=' '' ']'
   Line 271: local 'not_in_string=not in final'
   Line 272: local redefined_string=redefined
   Line 273: local redundant_string=redundant
   Line 278: local 'all_configs=/root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/9p.conf
/root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/acpi.conf
/root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/base.conf
/root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/cgroup.conf
/root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/cpu.conf
/root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/crypto.conf
/root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/dax.conf
/root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/debug.conf
/root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/elf.conf
/root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/fs.conf
/root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/hotplug.conf
/root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/huge.conf
/root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/lsm.conf
/root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/mem_agent.conf
/root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/mmio.conf
/root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/mmu.conf
/root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/namespaces.conf
/root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/netfilter.conf
/root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/network.conf
/root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/pmem.conf
/root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/seccomp.conf
/root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/security.conf
/root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/serial.conf
/root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/vfio.conf
/root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/virtio-extras.conf
/root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/virtio.conf /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/acpi.conf
/root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/base.conf
/root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/crypto.conf
/root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/dt.conf
/root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/erratum.conf
/root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/network.conf
/root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/numa.conf
/root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/pci.conf
/root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/ptp.conf
/root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/rtc.conf
/root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/serial.conf
/root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/virtio.conf'
   Line 279: [[ '' != '' ]]
   Line 283: [[ '' != '' ]]
   Line 294: [[ '' != '' ]]
   Line 300: [[ false == \t\r\u\e ]]
   Line 307: [[ '' != '' ]]
   Line 316: [[ '' != '' ]]
   Line 323: [[ no == \y\e\s ]]
   Line 329: [[ true == \t\r\u\e ]]
   Line 330: info 'Remove existing config /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/.config due to '\''-f'\'''
   Line 52: echo 'INFO: Remove existing config /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/.config due to '\''-f'\'''
INFO: Remove existing config /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/.config due to '-f'
   Line 331: '[' -f /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/.config ']'
   Line 332: '[' -f /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/.config.old ']'
   Line 335: info 'Constructing config from fragments: /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/.config'
   Line 52: echo 'INFO: Constructing config from fragments: /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/.config'
INFO: Constructing config from fragments: /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/.config
   Line 338: export KCONFIG_CONFIG=/root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/.config
   Line 338: KCONFIG_CONFIG=/root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/.config
   Line 339: export ARCH=arm64
   Line 339: ARCH=arm64
   Line 340: cd /root/kata-containers/tools/packaging/kernel/kata-linux-6.12.47-182
   Line 342: local results
    Line 343: /root/kata-containers/tools/packaging/kernel/kata-linux-6.12.47-182/scripts/kconfig/merge_config.sh -r -n /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/9p.conf /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/acpi.conf /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/base.conf /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/cgroup.conf /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/cpu.conf /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/crypto.conf /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/dax.conf /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/debug.conf /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/elf.conf /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/fs.conf /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/hotplug.conf /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/huge.conf /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/lsm.conf /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/mem_agent.conf /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/mmio.conf /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/mmu.conf /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/namespaces.conf /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/netfilter.conf /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/network.conf /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/pmem.conf /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/seccomp.conf /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/security.conf /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/serial.conf /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/vfio.conf /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/virtio-extras.conf /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/virtio.conf /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/acpi.conf /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/base.conf /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/crypto.conf /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/dt.conf /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/erratum.conf /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/network.conf /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/numa.conf /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/pci.conf /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/ptp.conf /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/rtc.conf /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/serial.conf /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/virtio.conf
   Line 343: results='Using /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/9p.conf as base
Merging /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/acpi.conf
Merging /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/base.conf
Merging /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/cgroup.conf
Value of CONFIG_CGROUP_PERF is redefined by fragment /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/cgroup.conf:
Previous value: # CONFIG_CGROUP_PERF needs
New value: CONFIG_CGROUP_PERF=y

Merging /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/cpu.conf
Merging /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/crypto.conf
Merging /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/dax.conf
Value of CONFIG_BLOCK is redundant by fragment /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/dax.conf:
Value of CONFIG_BLK_DEV is redundant by fragment /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/dax.conf:
Merging /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/debug.conf
Merging /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/elf.conf
Merging /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/fs.conf
Value of CONFIG_BLK_DEV_LOOP is redefined by fragment /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/fs.conf:
Previous value: # CONFIG_BLK_DEV_LOOP needs
New value: CONFIG_BLK_DEV_LOOP=y

Merging /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/hotplug.conf
Merging /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/huge.conf
Merging /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/lsm.conf
Merging /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/mem_agent.conf
Value of CONFIG_DEBUG_FS is redundant by fragment /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/mem_agent.conf:
Merging /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/mmio.conf
Merging /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/mmu.conf
Merging /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/namespaces.conf
Merging /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/netfilter.conf
Merging /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/network.conf
Merging /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/pmem.conf
Merging /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/seccomp.conf
Merging /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/security.conf
Merging /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/serial.conf
Merging /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/vfio.conf
Merging /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/virtio-extras.conf
Merging /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/../common/virtio.conf
Merging /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/acpi.conf
Merging /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/base.conf
Value of CONFIG_PERF_EVENTS is redundant by fragment /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/base.conf:
Merging /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/crypto.conf
Merging /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/dt.conf
Merging /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/erratum.conf
Merging /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/network.conf
Merging /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/numa.conf
Merging /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/pci.conf
Merging /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/ptp.conf
Merging /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/rtc.conf
Merging /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/serial.conf
Merging /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/virtio.conf
  HOSTCC  scripts/basic/fixdep
  HOSTCC  scripts/kconfig/conf.o
  HOSTCC  scripts/kconfig/confdata.o
  HOSTCC  scripts/kconfig/expr.o
  LEX     scripts/kconfig/lexer.lex.c
  YACC    scripts/kconfig/parser.tab.[ch]
  HOSTCC  scripts/kconfig/lexer.lex.o
  HOSTCC  scripts/kconfig/menu.o
  HOSTCC  scripts/kconfig/parser.tab.o
  HOSTCC  scripts/kconfig/preprocess.o
  HOSTCC  scripts/kconfig/symbol.o
  HOSTCC  scripts/kconfig/util.o
  HOSTLD  scripts/kconfig/conf
#
\# configuration written to /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/.config
#
Value requested for CONFIG_MEMCG_SWAP not in final .config
Requested value:  CONFIG_MEMCG_SWAP=y
Actual value:

Value requested for CONFIG_MEMCG_SWAP_ENABLED not in final .config
Requested value:  CONFIG_MEMCG_SWAP_ENABLED=y
Actual value:

Value requested for CONFIG_CRYPTO_SELFTESTS not in final .config
Requested value:  CONFIG_CRYPTO_SELFTESTS=y
Actual value:

Value requested for CONFIG_CRC_OPTIMIZATIONS not in final .config
Requested value:  CONFIG_CRC_OPTIMIZATIONS=y
Actual value:

Value requested for CONFIG_MHP_DEFAULT_ONLINE_TYPE_ONLINE_AUTO not in final .config
Requested value:  CONFIG_MHP_DEFAULT_ONLINE_TYPE_ONLINE_AUTO=y
Actual value:

Value requested for CONFIG_NETFILTER_XTABLES_LEGACY not in final .config
Requested value:  CONFIG_NETFILTER_XTABLES_LEGACY=y
Actual value:

Value requested for CONFIG_NF_LOG_COMMON not in final .config
Requested value:  CONFIG_NF_LOG_COMMON=y
Actual value:

Value requested for CONFIG_NF_NAT_NEEDED not in final .config
Requested value:  CONFIG_NF_NAT_NEEDED=y
Actual value:

Value requested for CONFIG_NF_NAT_PROTO_DCCP not in final .config
Requested value:  CONFIG_NF_NAT_PROTO_DCCP=y
Actual value:

Value requested for CONFIG_NF_NAT_PROTO_UDPLITE not in final .config
Requested value:  CONFIG_NF_NAT_PROTO_UDPLITE=y
Actual value:

Value requested for CONFIG_NF_NAT_PROTO_SCTP not in final .config
Requested value:  CONFIG_NF_NAT_PROTO_SCTP=y
Actual value:

Value requested for CONFIG_NF_NAT_PROTO_GRE not in final .config
Requested value:  CONFIG_NF_NAT_PROTO_GRE=y
Actual value:

Value requested for CONFIG_NF_NAT_IPV4 not in final .config
Requested value:  CONFIG_NF_NAT_IPV4=y
Actual value:

Value requested for CONFIG_GENERIC_MSI_IRQ_DOMAIN not in final .config
Requested value:  CONFIG_GENERIC_MSI_IRQ_DOMAIN=y
Actual value:

Value requested for CONFIG_ARM64_CRYPTO not in final .config
Requested value:  CONFIG_ARM64_CRYPTO=y
Actual value:

Value requested for CONFIG_HAVE_NET_DSA not in final .config
Requested value:  CONFIG_HAVE_NET_DSA=y
Actual value:

Value requested for CONFIG_PCI_MSI_IRQ_DOMAIN not in final .config
Requested value:  CONFIG_PCI_MSI_IRQ_DOMAIN=y
Actual value:     '
    Line 345: grep 'not in final'
   Line 345: results='Value requested for CONFIG_MEMCG_SWAP not in final .config
Value requested for CONFIG_MEMCG_SWAP_ENABLED not in final .config
Value requested for CONFIG_CRYPTO_SELFTESTS not in final .config
Value requested for CONFIG_CRC_OPTIMIZATIONS not in final .config
Value requested for CONFIG_MHP_DEFAULT_ONLINE_TYPE_ONLINE_AUTO not in final .config
Value requested for CONFIG_NETFILTER_XTABLES_LEGACY not in final .config
Value requested for CONFIG_NF_LOG_COMMON not in final .config
Value requested for CONFIG_NF_NAT_NEEDED not in final .config
Value requested for CONFIG_NF_NAT_PROTO_DCCP not in final .config
Value requested for CONFIG_NF_NAT_PROTO_UDPLITE not in final .config
Value requested for CONFIG_NF_NAT_PROTO_SCTP not in final .config
Value requested for CONFIG_NF_NAT_PROTO_GRE not in final .config
Value requested for CONFIG_NF_NAT_IPV4 not in final .config
Value requested for CONFIG_GENERIC_MSI_IRQ_DOMAIN not in final .config
Value requested for CONFIG_ARM64_CRYPTO not in final .config
Value requested for CONFIG_HAVE_NET_DSA not in final .config
Value requested for CONFIG_PCI_MSI_IRQ_DOMAIN not in final .config'
    Line 347: grep -v -f /root/kata-containers/tools/packaging/kernel/configs/fragments/whitelist.conf
   Line 347: results=
   Line 348: local version_config_whitelist=/root/kata-containers/tools/packaging/kernel/configs/fragments/whitelist-6.12.47.conf
   Line 349: '[' -f /root/kata-containers/tools/packaging/kernel/configs/fragments/whitelist-6.12.47.conf ']'
   Line 353: [[ false == \t\r\u\e ]]
    Line 356: echo
    Line 356: grep -v -q 'not in final'
    Line 356: echo 0
   Line 356: local missing=0
   Line 357: '[' 0 -ne 0 ']'
    Line 365: echo
    Line 365: grep -v -q redefined
    Line 365: echo 0
   Line 365: local redefined=0
   Line 366: '[' 0 -ne 0 ']'
    Line 375: echo
    Line 375: grep -v -q redundant
    Line 375: echo 0
   Line 375: local redundant=0
   Line 376: '[' 0 -ne 0 ']'
   Line 383: echo /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/.config
  Line 404: config=/root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/.config
  Line 410: '[' -f /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/.config ']'
  Line 411: echo /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/.config
 Line 486: kernel_config_path=/root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/.config
 Line 488: info 'Copying config file from: /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/.config'
 Line 52: echo 'INFO: Copying config file from: /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/.config'
INFO: Copying config file from: /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/.config
 Line 489: cp /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/.config ./.config
 Line 490: ARCH=arm64
 Line 490: make oldconfig
#
# No change to .config
#
 Line 493: info 'Fetching NVIDIA driver source code'
 Line 52: echo 'INFO: Fetching NVIDIA driver source code'
INFO: Fetching NVIDIA driver source code
 Line 494: [[ '' == \n\v\i\d\i\a ]]
 Line 765: '[' -d /root/kata-containers/tools/packaging/kernel/kata-linux-6.12.47-182 ']'
 Line 766: echo 'Kernel source ready: /root/kata-containers/tools/packaging/kernel/kata-linux-6.12.47-182 '
Kernel source ready: /root/kata-containers/tools/packaging/kernel/kata-linux-6.12.47-182

#### root@rpi4-desktop:~/kata-containers/tools/packaging/kernel# sudo ./build-kernel.sh -a aarch64 -v 6.12.47 -f -d build && sudo ./build-kernel.sh -a aarch64 -v 6.12.47 -d install
 Line 623: getopts a:b:c:dD:eEfg:hH:k:mp:r:st:u:v:x opt
 Line 695: shift 6
 Line 697: subcmd=build
 Line 699: '[' -z build ']'
 Line 701: [[ '' == \e\x\p\e\r\i\m\e\n\t\a\l ]]
 Line 712: '[' -z 6.12.47 ']'
 Line 737: kernel_version=6.12.47
 Line 739: '[' -z '' ']'
  Line 740: get_config_version
  Line 421: get_config_and_patches
  Line 415: '[' -z '' ']'
  Line 416: patches_path=/root/kata-containers/tools/packaging/kernel/patches
  Line 422: config_version_file=/root/kata-containers/tools/packaging/kernel/patches/../kata_config_version
  Line 423: '[' -f /root/kata-containers/tools/packaging/kernel/patches/../kata_config_version ']'
  Line 424: cat /root/kata-containers/tools/packaging/kernel/patches/../kata_config_version
 Line 740: config_version=182
 Line 741: [[ '' != '' ]]
 Line 744: kernel_path=/root/kata-containers/tools/packaging/kernel/kata-linux-6.12.47-182
 Line 746: info 'Config version: 182'
 Line 52: echo 'INFO: Config version: 182'
INFO: Config version: 182
 Line 749: info 'Kernel version: 6.12.47'
 Line 52: echo 'INFO: Kernel version: 6.12.47'
INFO: Kernel version: 6.12.47
  Line 751: uname -m
 Line 751: '[' aarch64 '!=' '' -a aarch64 '!=' aarch64 ']'
 Line 753: case "${subcmd}" in
 Line 755: build_kernel /root/kata-containers/tools/packaging/kernel/kata-linux-6.12.47-182
 Line 507: local kernel_path=/root/kata-containers/tools/packaging/kernel/kata-linux-6.12.47-182
 Line 508: '[' -n /root/kata-containers/tools/packaging/kernel/kata-linux-6.12.47-182 ']'
 Line 509: '[' -d /root/kata-containers/tools/packaging/kernel/kata-linux-6.12.47-182 ']'
 Line 510: '[' -n aarch64 ']'
  Line 511: arch_to_kernel aarch64
  Line 125: local -r arch=aarch64
  Line 127: case "$arch" in
  Line 128: echo arm64
 Line 511: arch_target=arm64
 Line 512: pushd /root/kata-containers/tools/packaging/kernel/kata-linux-6.12.47-182
  Line 513: nproc
 Line 513: make -j 4 ARCH=arm64
  SYNC    include/config/auto.conf.cmd
  WRAP    arch/arm64/include/generated/uapi/asm/kvm_para.h
  UPD     include/generated/uapi/linux/version.h
  WRAP    arch/arm64/include/generated/uapi/asm/errno.h
  WRAP    arch/arm64/include/generated/uapi/asm/ioctl.h
  WRAP    arch/arm64/include/generated/uapi/asm/ioctls.h
  WRAP    arch/arm64/include/generated/uapi/asm/ipcbuf.h
  WRAP    arch/arm64/include/generated/uapi/asm/msgbuf.h
  WRAP    arch/arm64/include/generated/uapi/asm/poll.h
  WRAP    arch/arm64/include/generated/uapi/asm/resource.h
  WRAP    arch/arm64/include/generated/uapi/asm/sembuf.h
  UPD     include/config/kernel.release
  WRAP    arch/arm64/include/generated/uapi/asm/shmbuf.h
  WRAP    arch/arm64/include/generated/uapi/asm/siginfo.h
  HOSTCC  scripts/dtc/dtc.o
  UPD     include/generated/compile.h
  WRAP    arch/arm64/include/generated/uapi/asm/socket.h
  WRAP    arch/arm64/include/generated/uapi/asm/sockios.h
  WRAP    arch/arm64/include/generated/uapi/asm/stat.h
  WRAP    arch/arm64/include/generated/uapi/asm/swab.h
  HOSTCC  scripts/dtc/flattree.o
  WRAP    arch/arm64/include/generated/uapi/asm/termbits.h
  WRAP    arch/arm64/include/generated/uapi/asm/termios.h
  WRAP    arch/arm64/include/generated/uapi/asm/types.h
  SYSHDR  arch/arm64/include/generated/uapi/asm/unistd_64.h
  UPD     include/generated/utsrelease.h
  HOSTCC  scripts/dtc/fstree.o
  WRAP    arch/arm64/include/generated/asm/early_ioremap.h
  WRAP    arch/arm64/include/generated/asm/mcs_spinlock.h
  WRAP    arch/arm64/include/generated/asm/mmzone.h
  WRAP    arch/arm64/include/generated/asm/qrwlock.h
  WRAP    arch/arm64/include/generated/asm/qspinlock.h
  WRAP    arch/arm64/include/generated/asm/parport.h
  WRAP    arch/arm64/include/generated/asm/user.h
  WRAP    arch/arm64/include/generated/asm/cfi.h
  WRAP    arch/arm64/include/generated/asm/delay.h
  WRAP    arch/arm64/include/generated/asm/div64.h
  WRAP    arch/arm64/include/generated/asm/dma-mapping.h
  WRAP    arch/arm64/include/generated/asm/dma.h
  WRAP    arch/arm64/include/generated/asm/emergency-restart.h
  WRAP    arch/arm64/include/generated/asm/hw_irq.h
  WRAP    arch/arm64/include/generated/asm/irq_regs.h
  WRAP    arch/arm64/include/generated/asm/kdebug.h
  WRAP    arch/arm64/include/generated/asm/kmap_size.h
  WRAP    arch/arm64/include/generated/asm/local.h
  WRAP    arch/arm64/include/generated/asm/local64.h
  WRAP    arch/arm64/include/generated/asm/mmiowb.h
  WRAP    arch/arm64/include/generated/asm/msi.h
  WRAP    arch/arm64/include/generated/asm/serial.h
  WRAP    arch/arm64/include/generated/asm/softirq_stack.h
  WRAP    arch/arm64/include/generated/asm/switch_to.h
  WRAP    arch/arm64/include/generated/asm/trace_clock.h
  WRAP    arch/arm64/include/generated/asm/vga.h
  WRAP    arch/arm64/include/generated/asm/video.h
  SYSTBL  arch/arm64/include/generated/asm/syscall_table_32.h
  HOSTCC  scripts/dtc/data.o
  SYSTBL  arch/arm64/include/generated/asm/syscall_table_64.h
  SYSHDR  arch/arm64/include/generated/asm/unistd_32.h
  SYSHDR  arch/arm64/include/generated/asm/unistd_compat_32.h
  HOSTCC  scripts/dtc/livetree.o
  HOSTCC  scripts/dtc/treesource.o
  HOSTCC  scripts/dtc/srcpos.o
  HOSTCC  scripts/dtc/checks.o
  HOSTCC  scripts/dtc/util.o
  LEX     scripts/dtc/dtc-lexer.lex.c
  YACC    scripts/dtc/dtc-parser.tab.[ch]
  HOSTCC  scripts/dtc/libfdt/fdt.o
  HOSTCC  scripts/dtc/libfdt/fdt_ro.o
  HOSTCC  scripts/dtc/libfdt/fdt_wip.o
  HOSTCC  scripts/dtc/libfdt/fdt_sw.o
  HOSTCC  scripts/dtc/libfdt/fdt_rw.o
  HOSTCC  scripts/dtc/libfdt/fdt_strerror.o
  HOSTCC  scripts/dtc/libfdt/fdt_empty_tree.o
  HOSTCC  scripts/dtc/libfdt/fdt_addresses.o
  HOSTCC  scripts/dtc/libfdt/fdt_overlay.o
  HOSTCC  scripts/dtc/fdtoverlay.o
  HOSTCC  scripts/dtc/dtc-lexer.lex.o
  HOSTCC  scripts/dtc/dtc-parser.tab.o
  HOSTLD  scripts/dtc/fdtoverlay
  HOSTLD  scripts/dtc/dtc
  HOSTCC  scripts/kallsyms
  HOSTCC  scripts/sorttable
  HOSTCC  scripts/selinux/genheaders/genheaders
  HOSTCC  scripts/selinux/mdp/mdp
  HOSTCC  scripts/asn1_compiler
  GEN     arch/arm64/include/generated/asm/cpucap-defs.h
  GEN     arch/arm64/include/generated/asm/sysreg-defs.h
  CC      scripts/mod/empty.o
  HOSTCC  scripts/mod/mk_elfconfig
  CC      scripts/mod/devicetable-offsets.s
  UPD     scripts/mod/devicetable-offsets.h
  MKELF   scripts/mod/elfconfig.h
  HOSTCC  scripts/mod/modpost.o
  HOSTCC  scripts/mod/file2alias.o
  HOSTCC  scripts/mod/sumversion.o
  HOSTCC  scripts/mod/symsearch.o
  HOSTLD  scripts/mod/modpost
  CC      kernel/bounds.s
  CHKSHA1 include/linux/atomic/atomic-arch-fallback.h
  CHKSHA1 include/linux/atomic/atomic-instrumented.h
  UPD     include/generated/timeconst.h
  CHKSHA1 include/linux/atomic/atomic-long.h
  UPD     include/generated/bounds.h
  CC      arch/arm64/kernel/asm-offsets.s
  UPD     include/generated/asm-offsets.h
  CALL    scripts/checksyscalls.sh
  LDS     arch/arm64/kernel/vdso/vdso.lds
  CC      arch/arm64/kernel/vdso/vgettimeofday.o
  AS      arch/arm64/kernel/vdso/note.o
  AS      arch/arm64/kernel/vdso/sigreturn.o
  CC      arch/arm64/kernel/vdso/vgetrandom.o
  AS      arch/arm64/kernel/vdso/vgetrandom-chacha.o
  LD      arch/arm64/kernel/vdso/vdso.so.dbg
  VDSOSYM include/generated/vdso-offsets.h
  OBJCOPY arch/arm64/kernel/vdso/vdso.so
  HOSTCC  usr/gen_init_cpio
  CC      init/main.o
  CC      arch/arm64/kernel/pi/idreg-override.o
  CC      kernel/sched/core.o
  GEN     usr/initramfs_data.cpio
  COPY    usr/initramfs_inc_data
  AS      usr/initramfs_data.o
  AR      usr/built-in.a
  AR      certs/built-in.a
  CC      kernel/locking/mutex.o
  CC      arch/arm64/kernel/pi/map_kernel.o
  CC      arch/arm64/kernel/pi/map_range.o
  UPD     init/utsversion-tmp.h
  CC      init/do_mounts.o
  CC      kernel/locking/semaphore.o
  CC      arch/arm64/kernel/pi/lib-fdt.o
  CC      arch/arm64/kernel/pi/lib-fdt_ro.o
  CC      kernel/locking/rwsem.o
  CC      arch/arm64/kernel/pi/relocate.o
  CC      init/do_mounts_rd.o
  CC      arch/arm64/kernel/pi/kaslr_early.o
  HOSTCC  arch/arm64/kernel/pi/relacheck
  CC      kernel/locking/percpu-rwsem.o
  OBJCOPY arch/arm64/kernel/pi/idreg-override.pi.o
  OBJCOPY arch/arm64/kernel/pi/map_kernel.pi.o
  OBJCOPY arch/arm64/kernel/pi/map_range.pi.o
  OBJCOPY arch/arm64/kernel/pi/lib-fdt.pi.o
  OBJCOPY arch/arm64/kernel/pi/lib-fdt_ro.pi.o
  OBJCOPY arch/arm64/kernel/pi/relocate.pi.o
  OBJCOPY arch/arm64/kernel/pi/kaslr_early.pi.o
  AR      arch/arm64/kernel/pi/built-in.a
  AR      arch/arm64/kernel/probes/built-in.a
  LDS     arch/arm64/kernel/vmlinux.lds
  CC      arch/arm64/kernel/debug-monitors.o
  CC      init/do_mounts_initrd.o
  CC      kernel/locking/spinlock.o
  CC      kernel/locking/osq_lock.o
  AS      arch/arm64/kernel/entry.o
  CC      arch/arm64/kernel/irq.o
  CC      kernel/locking/qspinlock.o
  CC      kernel/sched/fair.o
  CC      init/initramfs.o
  CC      arch/arm64/kernel/fpsimd.o
  CC      kernel/locking/rtmutex_api.o
  CC      init/calibrate.o
  CC      init/init_task.o
  CC      arch/arm64/kernel/entry-common.o
  CC      kernel/locking/qrwlock.o
  CC      init/version.o
  AR      init/built-in.a
  CC      mm/filemap.o
  AR      kernel/locking/built-in.a
  CC      kernel/power/qos.o
  AS      arch/arm64/kernel/entry-fpsimd.o
  CC      arch/arm64/kernel/process.o
  CC      kernel/power/process.o
  CC      arch/arm64/kernel/ptrace.o
  AR      kernel/power/built-in.a
  CC      arch/arm64/kernel/setup.o
  CC      kernel/sched/build_policy.o
  CC      kernel/printk/printk.o
  CC      arch/arm64/kernel/signal.o
  CC      mm/mempool.o
  CC      mm/oom_kill.o
  CC      arch/arm64/kernel/sys.o
  CC      arch/arm64/kernel/stacktrace.o
  CC      kernel/printk/printk_safe.o
  CC      mm/fadvise.o
  CC      kernel/printk/nbcon.o
  CC      arch/arm64/kernel/time.o
  CC      mm/maccess.o
  CC      kernel/printk/printk_ringbuffer.o
  CC      arch/arm64/kernel/traps.o
  CC      kernel/printk/sysctl.o
  CC      mm/page-writeback.o
  CC      kernel/sched/build_utility.o
  AR      kernel/printk/built-in.a
  CC      mm/folio-compat.o
  CC      arch/arm64/kernel/io.o
  CC      mm/readahead.o
  CC      arch/arm64/kernel/vdso.o
  AS      arch/arm64/kernel/hyp-stub.o
  CC      arch/arm64/kernel/psci.o
  CC      mm/swap.o
  CC      arch/arm64/mm/dma-mapping.o
  CC      arch/arm64/kernel/cpu_ops.o
  CC      arch/arm64/mm/extable.o
  CC      arch/arm64/kernel/return_address.o
  CC      arch/arm64/mm/fault.o
  CC      arch/arm64/kernel/cpuinfo.o
  CC      mm/truncate.o
  CC      arch/arm64/kernel/cpu_errata.o
  CC      arch/arm64/mm/init.o
  CC      arch/arm64/kernel/cpufeature.o
  AR      kernel/sched/built-in.a
  CC      kernel/irq/irqdesc.o
  CC      mm/vmscan.o
  AS      arch/arm64/mm/cache.o
  CC      arch/arm64/mm/copypage.o
  CC      kernel/irq/handle.o
  CC      arch/arm64/mm/flush.o
  CC      arch/arm64/kernel/alternative.o
  CC      kernel/irq/manage.o
  CC      arch/arm64/mm/ioremap.o
  CC      arch/arm64/mm/mmap.o
  CC      arch/arm64/kernel/cacheinfo.o
  CC      arch/arm64/mm/pgd.o
  CC      arch/arm64/kernel/smp.o
  CC      arch/arm64/mm/mem_encrypt.o
  CC      kernel/irq/spurious.o
  CC      arch/arm64/mm/mmu.o
  CC      kernel/irq/resend.o
  CC      arch/arm64/kernel/smp_spin_table.o
  CC      kernel/irq/chip.o
  CC      arch/arm64/kernel/topology.o
  CC      arch/arm64/mm/context.o
  CC      mm/shrinker.o
  AS      arch/arm64/kernel/smccc-call.o
  CC      arch/arm64/kernel/syscall.o
  CC      kernel/irq/dummychip.o
  AS      arch/arm64/mm/proc.o
  CC      arch/arm64/mm/pageattr.o
  CC      kernel/irq/devres.o
  CC      arch/arm64/kernel/proton-pack.o
  CC      mm/shmem.o
  CC      arch/arm64/mm/fixmap.o
  CC      kernel/irq/autoprobe.o
  CC      arch/arm64/mm/hugetlbpage.o
  CC      kernel/irq/irqdomain.o
  CC      arch/arm64/kernel/idle.o
  CC      arch/arm64/kernel/patching.o
  AR      arch/arm64/mm/built-in.a
  AR      arch/arm64/net/built-in.a
  CC      kernel/irq/proc.o
  CC      kernel/rcu/update.o
  CC      arch/arm64/kernel/perf_regs.o
  CC      kernel/irq/cpuhotplug.o
  CC      mm/util.o
  CC      arch/arm64/kernel/perf_callchain.o
  CC      kernel/irq/msi.o
  CC      arch/arm64/kernel/hw_breakpoint.o
  CC      kernel/rcu/sync.o
  CC      mm/mmzone.o
  CC      kernel/rcu/srcutree.o
  CC      mm/vmstat.o
  AS      arch/arm64/kernel/sleep.o
  CC      arch/arm64/kernel/suspend.o
  CC      kernel/irq/ipi.o
  CC      arch/arm64/kernel/efi.o
  CC      kernel/irq/affinity.o
  CC      kernel/rcu/tree.o
  AS      arch/arm64/kernel/efi-rt-wrapper.o
  AR      kernel/irq/built-in.a
  CC      arch/arm64/kernel/pci.o
  CC      fs/notify/dnotify/dnotify.o
  CC      mm/backing-dev.o
  CC      arch/arm64/kernel/acpi.o
  AR      fs/notify/dnotify/built-in.a
  CC      fs/notify/inotify/inotify_fsnotify.o
  CC      fs/notify/inotify/inotify_user.o
  CC      arch/arm64/kernel/acpi_numa.o
  CC      mm/mm_init.o
  CC      arch/arm64/kernel/paravirt.o
  AR      fs/notify/inotify/built-in.a
  CC      fs/notify/fanotify/fanotify.o
  CC      arch/arm64/kernel/kaslr.o
  CC      arch/arm64/kernel/elfcore.o
  AS      arch/arm64/kernel/vdso-wrap.o
  AS      arch/arm64/kernel/head.o
  AR      arch/arm64/kernel/built-in.a
  AS      arch/arm64/crypto/aes-ce-core.o
  CC      arch/arm64/crypto/aes-ce-glue.o
  CC      mm/percpu.o
  CC      fs/notify/fanotify/fanotify_user.o
  AS      arch/arm64/crypto/aes-cipher-core.o
  CC      arch/arm64/crypto/aes-cipher-glue.o
  AR      arch/arm64/crypto/built-in.a
  AR      arch/arm64/built-in.a
  CC      fs/iomap/trace.o
  CC      kernel/rcu/rcu_segcblist.o
  AR      fs/notify/fanotify/built-in.a
  CC      fs/notify/fsnotify.o
  CC      fs/iomap/iter.o
  AR      kernel/rcu/built-in.a
  AR      kernel/livepatch/built-in.a
  CC      kernel/dma/mapping.o
  CC      fs/iomap/buffered-io.o
  CC      mm/slab_common.o
  CC      fs/notify/notification.o
  CC      kernel/dma/direct.o
  CC      fs/notify/group.o
  CC      mm/compaction.o
  CC      fs/notify/mark.o
  CC      kernel/dma/ops_helpers.o
  CC      fs/iomap/direct-io.o
  CC      kernel/dma/coherent.o
  CC      fs/notify/fdinfo.o
  CC      kernel/dma/swiotlb.o
  CC      fs/iomap/fiemap.o
  AR      fs/notify/built-in.a
  AR      kernel/entry/built-in.a
  AR      fs/quota/built-in.a
  CC      mm/show_mem.o
  CC      fs/iomap/seek.o
  CC      kernel/time/time.o
  CC      kernel/dma/pool.o
  CC      mm/interval_tree.o
  CC      fs/iomap/swapfile.o
  CC      kernel/time/timer.o
  CC      kernel/dma/remap.o
  AR      fs/iomap/built-in.a
  CC      fs/proc/task_mmu.o
  CC      mm/list_lru.o
  AR      kernel/dma/built-in.a
  CC      fs/proc/inode.o
  CC      kernel/time/hrtimer.o
  CC      fs/proc/root.o
  CC      mm/workingset.o
  CC      fs/proc/base.o
  CC      ipc/util.o
  CC      mm/debug.o
  CC      kernel/time/timekeeping.o
  CC      mm/gup.o
  CC      ipc/msgutil.o
  CC      kernel/time/ntp.o
  CC      ipc/msg.o
  CC      fs/proc/generic.o
  CC      kernel/time/clocksource.o
  CC      fs/proc/array.o
  CC      ipc/sem.o
  CC      mm/mmap_lock.o
  CC      kernel/time/jiffies.o
  CC      kernel/time/timer_list.o
  CC      fs/proc/fd.o
  CC      mm/highmem.o
  CC      kernel/time/timeconv.o
  CC      mm/memory.o
  CC      fs/proc/proc_tty.o
  CC      kernel/time/timecounter.o
  CC      kernel/time/alarmtimer.o
  CC      ipc/shm.o
  CC      fs/proc/cmdline.o
  CC      fs/proc/consoles.o
  CC      kernel/time/posix-timers.o
  CC      fs/proc/cpuinfo.o
  CC      ipc/syscall.o
  CC      fs/proc/devices.o
  CC      kernel/time/posix-cpu-timers.o
  CC      ipc/ipc_sysctl.o
  CC      fs/proc/interrupts.o
  CC      ipc/mqueue.o
  CC      fs/proc/loadavg.o
  CC      kernel/time/posix-clock.o
  CC      fs/proc/meminfo.o
  CC      kernel/time/itimer.o
  CC      mm/mincore.o
  CC      fs/proc/stat.o
  CC      ipc/namespace.o
  CC      fs/proc/uptime.o
  CC      kernel/time/clockevents.o
  CC      mm/mlock.o
  CC      ipc/mq_sysctl.o
  CC      fs/proc/util.o
  AR      ipc/built-in.a
  CC      kernel/time/tick-common.o
  CC      kernel/futex/core.o
  CC      fs/proc/version.o
  CC      fs/proc/softirqs.o
  CC      kernel/time/tick-broadcast.o
  CC      mm/mmap.o
  CC      kernel/futex/syscalls.o
  CC      fs/proc/namespaces.o
  CC      kernel/time/tick-broadcast-hrtimer.o
  CC      kernel/futex/pi.o
  CC      fs/proc/self.o
  CC      kernel/time/sched_clock.o
  CC      fs/proc/thread_self.o
  CC      mm/mmu_gather.o
  CC      kernel/futex/requeue.o
  CC      kernel/time/tick-oneshot.o
  CC      fs/proc/proc_sysctl.o
  CC      kernel/time/tick-sched.o
  CC      mm/mprotect.o
  CC      kernel/futex/waitwake.o
  AR      kernel/futex/built-in.a
  CC      kernel/cgroup/cgroup.o
  CC      kernel/time/timer_migration.o
  CC      mm/mremap.o
  CC      fs/proc/proc_net.o
  CC      kernel/time/vsyscall.o
  CC      fs/proc/kmsg.o
  CC      kernel/time/timekeeping_debug.o
  CC      mm/msync.o
  CC      fs/proc/page.o
  AR      kernel/time/built-in.a
  CC      fs/kernfs/mount.o
  CC      mm/page_vma_mapped.o
  AR      fs/proc/built-in.a
  CC      kernel/cgroup/rstat.o
  CC      fs/kernfs/inode.o
  CC      mm/pagewalk.o
  CC      kernel/cgroup/namespace.o
  CC      fs/kernfs/dir.o
  CC      mm/pgtable-generic.o
  CC      kernel/cgroup/cgroup-v1.o
  CC      security/keys/gc.o
  CC      mm/rmap.o
  CC      security/keys/key.o
  CC      fs/kernfs/file.o
  CC      kernel/cgroup/freezer.o
  CC      fs/kernfs/symlink.o
  CC      security/keys/keyring.o
  CC      kernel/cgroup/legacy_freezer.o
  CC      mm/vmalloc.o
  AR      fs/kernfs/built-in.a
  CC      fs/sysfs/file.o
  CC      kernel/cgroup/pids.o
  CC      security/keys/keyctl.o
  CC      fs/sysfs/dir.o
  CC      kernel/cgroup/cpuset.o
  CC      fs/sysfs/symlink.o
  CC      security/keys/permission.o
  CC      fs/sysfs/mount.o
  CC      security/keys/process_keys.o
  CC      fs/sysfs/group.o
  AR      fs/sysfs/built-in.a
  CC      fs/devpts/inode.o
  CC      mm/vma.o
  CC      security/keys/request_key.o
  AR      kernel/cgroup/built-in.a
  CC      kernel/bpf/core.o
  AR      fs/devpts/built-in.a
  CC      fs/netfs/buffered_read.o
  CC      security/keys/request_key_auth.o
  CC      mm/mseal.o
  CC      fs/netfs/buffered_write.o
  CC      security/keys/user_defined.o
  CC      mm/page_alloc.o
  CC      security/keys/proc.o
  CC      fs/netfs/direct_read.o
  CC      kernel/bpf/syscall.o
  CC      security/keys/sysctl.o
  CC      fs/netfs/direct_write.o
  AR      security/keys/built-in.a
  GEN     security/selinux/flask.h security/selinux/av_permissions.h
  CC      security/selinux/avc.o
  CC      fs/netfs/iterator.o
  CC      fs/netfs/locking.o
  CC      security/selinux/hooks.o
  CC      fs/netfs/main.o
  CC      fs/netfs/misc.o
  CC      mm/init-mm.o
  CC      kernel/bpf/verifier.o
  CC      mm/memblock.o
  CC      fs/netfs/objects.o
  CC      fs/netfs/read_collect.o
  CC      mm/memory_hotplug.o
  CC      fs/netfs/read_pgpriv2.o
  CC      security/selinux/selinuxfs.o
  CC      fs/netfs/read_retry.o
  CC      mm/slub.o
  CC      fs/netfs/write_collect.o
  CC      security/selinux/netlink.o
  CC      fs/netfs/write_issue.o
  CC      security/selinux/nlmsgtab.o
  AR      fs/netfs/built-in.a
  CC      fs/ext4/balloc.o
  CC      security/selinux/netif.o
  CC      fs/ext4/bitmap.o
  CC      security/selinux/netnode.o
  CC      mm/madvise.o
  CC      fs/ext4/block_validity.o
  CC      security/selinux/netport.o
  CC      fs/ext4/dir.o
  CC      mm/page_io.o
  CC      fs/ext4/ext4_jbd2.o
  CC      security/selinux/status.o
  CC      mm/swap_state.o
  CC      fs/ext4/extents.o
  CC      security/selinux/ss/ebitmap.o
  CC      mm/swapfile.o
  CC      security/selinux/ss/hashtab.o
  CC      security/selinux/ss/symtab.o
  CC      security/selinux/ss/sidtab.o
  CC      kernel/bpf/inode.o
  CC      fs/ext4/extents_status.o
  CC      security/selinux/ss/avtab.o
  CC      kernel/bpf/helpers.o
  CC      mm/swap_slots.o
  CC      security/selinux/ss/policydb.o
  CC      fs/ext4/file.o
  CC      mm/dmapool.o
  CC      kernel/bpf/tnum.o
  CC      mm/hugetlb.o
  CC      kernel/bpf/log.o
  CC      fs/ext4/fsmap.o
  CC      security/selinux/ss/services.o
  CC      kernel/bpf/token.o
  CC      fs/ext4/fsync.o
  CC      fs/ext4/hash.o
  CC      kernel/bpf/bpf_iter.o
  CC      fs/ext4/ialloc.o
  CC      kernel/bpf/map_iter.o
  CC      security/selinux/ss/conditional.o
  CC      kernel/bpf/task_iter.o
  CC      mm/mempolicy.o
  CC      fs/ext4/indirect.o
  CC      security/selinux/ss/mls.o
  CC      kernel/bpf/prog_iter.o
  CC      fs/ext4/inline.o
  CC      security/selinux/ss/context.o
  CC      kernel/bpf/link_iter.o
  AR      security/selinux/built-in.a
  CC      security/commoncap.o
  CC      mm/sparse.o
  CC      kernel/bpf/hashtab.o
  CC      fs/ext4/inode.o
  CC      mm/sparse-vmemmap.o
  CC      security/lsm_syscalls.o
  CC      mm/migrate.o
  CC      security/min_addr.o
  CC      security/security.o
  CC      kernel/bpf/arraymap.o
  CC      mm/memory-tiers.o
  CC      fs/ext4/ioctl.o
  CC      kernel/bpf/percpu_freelist.o
  CC      kernel/bpf/bpf_lru_list.o
  CC      mm/migrate_device.o
  CC      kernel/bpf/lpm_trie.o
  CC      security/lsm_audit.o
  CC      fs/ext4/mballoc.o
  CC      mm/page_counter.o
  CC      mm/memcontrol.o
  CC      kernel/bpf/map_in_map.o
  CC      security/device_cgroup.o
  CC      kernel/bpf/bloom_filter.o
  AR      security/built-in.a
  CC      fs/jbd2/transaction.o
  CC      kernel/bpf/local_storage.o
  CC      kernel/bpf/queue_stack_maps.o
  CC      fs/jbd2/commit.o
  CC      mm/vmpressure.o
  CC      fs/ext4/migrate.o
  CC      kernel/bpf/ringbuf.o
  CC      mm/swap_cgroup.o
  CC      fs/jbd2/recovery.o
  CC      fs/ext4/mmp.o
  CC      kernel/bpf/bpf_local_storage.o
  CC      mm/hugetlb_cgroup.o
  CC      fs/jbd2/checkpoint.o
  CC      fs/ext4/move_extent.o
  CC      mm/page_isolation.o
  CC      kernel/bpf/bpf_task_storage.o
  CC      fs/jbd2/revoke.o
  CC      fs/ext4/namei.o
  CC      mm/early_ioremap.o
  CC      fs/jbd2/journal.o
  CC      kernel/bpf/disasm.o
  CC      mm/numa.o
  CC      kernel/bpf/mprog.o
  CC      mm/numa_memblks.o
  CC      kernel/bpf/btf.o
  AR      fs/jbd2/built-in.a
  CC      mm/balloon_compaction.o
  CC      fs/ext4/page-io.o
  CC      crypto/api.o
  CC      mm/secretmem.o
  CC      crypto/cipher.o
  CC      fs/ext4/readpage.o
  CC      crypto/compress.o
  CC      mm/memremap.o
  CC      crypto/fips.o
  CC      fs/ext4/resize.o
  CC      crypto/algapi.o
  CC      mm/memfd.o
  CC      crypto/scatterwalk.o
  CC      mm/page_reporting.o
  CC      fs/ext4/super.o
  CC      crypto/proc.o
  CC      mm/ioremap.o
  CC      crypto/aead.o
  AR      mm/built-in.a
  CC      block/partitions/core.o
  CC      kernel/bpf/memalloc.o
  CC      crypto/geniv.o
  CC      block/partitions/msdos.o
  CC      crypto/lskcipher.o
  CC      kernel/bpf/arena.o
  CC      block/partitions/efi.o
  CC      crypto/skcipher.o
  AR      block/partitions/built-in.a
  CC      block/bdev.o
  CC      kernel/bpf/devmap.o
  CC      fs/ext4/symlink.o
  CC      fs/ext4/sysfs.o
  CC      crypto/bpf_crypto_skcipher.o
  CC      block/fops.o
  CC      crypto/seqiv.o
  CC      kernel/bpf/cpumap.o
  CC      fs/ext4/xattr.o
  CC      crypto/echainiv.o
  CC      block/bio.o
  CC      crypto/ahash.o
  CC      kernel/bpf/offload.o
  CC      fs/ext4/xattr_hurd.o
  CC      crypto/shash.o
  CC      block/elevator.o
  CC      fs/ext4/xattr_trusted.o
  CC      kernel/bpf/net_namespace.o
  CC      crypto/akcipher.o
  CC      block/blk-core.o
  CC      fs/ext4/xattr_user.o
  CC      kernel/bpf/tcx.o
  CC      crypto/sig.o
  CC      fs/ext4/fast_commit.o
  CC      block/blk-sysfs.o
  CC      crypto/kpp.o
  CC      kernel/bpf/stackmap.o
  CC      crypto/acompress.o
  CC      fs/ext4/orphan.o
  CC      block/blk-flush.o
  CC      kernel/bpf/cgroup_iter.o
  CC      crypto/scompress.o
  CC      fs/ext4/acl.o
  CC      block/blk-settings.o
  CC      kernel/bpf/bpf_cgrp_storage.o
  CC      crypto/algboss.o
  CC      fs/ext4/xattr_security.o
  CC      block/blk-ioc.o
  CC      kernel/bpf/cgroup.o
  AR      fs/ext4/built-in.a
  CC      fs/ramfs/inode.o
  CC      crypto/testmgr.o
  CC      block/blk-map.o
  CC      fs/ramfs/file-mmu.o
  CC      block/blk-merge.o
  AR      fs/ramfs/built-in.a
  CC      fs/hugetlbfs/inode.o
  CC      kernel/bpf/reuseport_array.o
  CC      crypto/hmac.o
  CC      block/blk-timeout.o
  CC      crypto/crypto_null.o
  AR      fs/hugetlbfs/built-in.a
  CC      fs/exportfs/expfs.o
  CC      kernel/bpf/crypto.o
  CC      crypto/md5.o
  CC      block/blk-lib.o
  AR      fs/exportfs/built-in.a
  CC      fs/nls/nls_base.o
  CC      crypto/sha256_generic.o
  AR      fs/nls/built-in.a
  AR      fs/unicode/built-in.a
  CC      block/blk-mq.o
  CC      fs/autofs/init.o
  CC      kernel/bpf/relo_core.o
  CC      crypto/sha512_generic.o
  CC      fs/autofs/inode.o
  CC      crypto/sha3_generic.o
  CC      crypto/ecb.o
  CC      kernel/bpf/btf_iter.o
  CC      fs/autofs/root.o
  CC      crypto/cbc.o
  CC      kernel/bpf/btf_relocate.o
  CC      crypto/ctr.o
  CC      fs/autofs/symlink.o
  CC      crypto/gcm.o
  AR      kernel/bpf/built-in.a
  CC      kernel/events/core.o
  CC      fs/autofs/waitq.o
  CC      block/blk-mq-tag.o
  CC      crypto/aes_generic.o
  CC      fs/autofs/expire.o
  CC      block/blk-stat.o
  CC      crypto/deflate.o
  CC      fs/autofs/dev-ioctl.o
  CC      block/blk-mq-sysfs.o
  CC      crypto/crc32c_generic.o
  CC      crypto/authenc.o
  AR      fs/autofs/built-in.a
  CC      block/blk-mq-cpumap.o
  CC      fs/fuse/dev.o
  CC      block/blk-mq-sched.o
  CC      crypto/authencesn.o
  CC      block/ioctl.o
  CC      crypto/rng.o
  CC      fs/fuse/dir.o
  CC      crypto/ansi_cprng.o
  CC      block/genhd.o
  CC      crypto/drbg.o
  CC      fs/fuse/file.o
  CC      block/ioprio.o
  CC      crypto/jitterentropy.o
  CC      crypto/jitterentropy-kcapi.o
  CC      kernel/events/ring_buffer.o
  CC      crypto/ghash-generic.o
  CC      block/badblocks.o
  CC      crypto/af_alg.o
  CC      kernel/events/callchain.o
  CC      block/blk-rq-qos.o
  CC      kernel/events/hw_breakpoint.o
  CC      fs/fuse/inode.o
  CC      block/disk-events.o
  CC      crypto/algif_hash.o
  CC      block/blk-ia-ranges.o
  AR      kernel/events/built-in.a
  CC      kernel/fork.o
  AR      crypto/built-in.a
  CC      io_uring/io_uring.o
  CC      fs/fuse/control.o
  CC      block/early-lookup.o
  CC      block/bsg.o
  CC      fs/fuse/xattr.o
  CC      block/blk-cgroup.o
  CC      fs/fuse/acl.o
  CC      kernel/exec_domain.o
  CC      fs/fuse/readdir.o
  CC      kernel/panic.o
  CC      io_uring/opdef.o
  CC      fs/fuse/ioctl.o
  CC      block/blk-cgroup-rwstat.o
  CC      kernel/cpu.o
  CC      io_uring/kbuf.o
  CC      block/blk-throttle.o
  CC      fs/fuse/iomode.o
  CC      fs/fuse/dax.o
  CC      io_uring/rsrc.o
  CC      block/blk-mq-pci.o
  CC      kernel/exit.o
  CC      fs/fuse/virtio_fs.o
  CC      block/blk-mq-virtio.o
  CC      io_uring/notif.o
  AR      block/built-in.a
  AS      arch/arm64/lib/clear_page.o
  AS      arch/arm64/lib/clear_user.o
  AS      arch/arm64/lib/copy_from_user.o
  AS      arch/arm64/lib/copy_page.o
  AS      arch/arm64/lib/copy_to_user.o
  CC      arch/arm64/lib/csum.o
  CC      arch/arm64/lib/delay.o
  CC      kernel/softirq.o
  CC      io_uring/tctx.o
  CC      arch/arm64/lib/insn.o
  AR      fs/fuse/built-in.a
  CC      fs/overlayfs/super.o
  CC      io_uring/filetable.o
  AS      arch/arm64/lib/memchr.o
  AS      arch/arm64/lib/memcmp.o
  CC      kernel/resource.o
  AS      arch/arm64/lib/memcpy.o
  AS      arch/arm64/lib/memset.o
  AS      arch/arm64/lib/strchr.o
  AS      arch/arm64/lib/strcmp.o
  AS      arch/arm64/lib/strlen.o
  AS      arch/arm64/lib/strncmp.o
  AS      arch/arm64/lib/strnlen.o
  AS      arch/arm64/lib/strrchr.o
  AS      arch/arm64/lib/tishift.o
  CC      arch/arm64/lib/uaccess_flushcache.o
  CC      io_uring/rw.o
  CC      fs/overlayfs/namei.o
  AS      arch/arm64/lib/crc32.o
  AR      arch/arm64/lib/lib.a
  AR      arch/arm64/lib/built-in.a
  CC      lib/math/div64.o
  CC      lib/math/gcd.o
  CC      lib/math/lcm.o
  CC      lib/math/int_log.o
  CC      lib/math/int_pow.o
  CC      kernel/sysctl.o
  CC      lib/math/int_sqrt.o
  CC      lib/math/reciprocal_div.o
  CC      lib/math/rational.o
  CC      io_uring/net.o
  CC      fs/overlayfs/util.o
  AR      lib/math/built-in.a
  CC      lib/crypto/memneq.o
  CC      lib/crypto/utils.o
  CC      lib/crypto/chacha.o
  CC      kernel/capability.o
  CC      lib/crypto/aes.o
  CC      fs/overlayfs/inode.o
  CC      lib/crypto/gf128mul.o
  CC      io_uring/poll.o
  CC      kernel/ptrace.o
  CC      lib/crypto/blake2s.o
  CC      fs/overlayfs/file.o
  CC      lib/crypto/blake2s-generic.o
  CC      lib/crypto/blake2s-selftest.o
  CC      io_uring/eventfd.o
  CC      kernel/user.o
  CC      lib/crypto/sha1.o
  CC      fs/overlayfs/dir.o
  CC      kernel/signal.o
  CC      lib/crypto/sha256.o
  CC      io_uring/uring_cmd.o
  AR      lib/crypto/built-in.a
  CC      lib/zlib_inflate/inffast.o
  CC      lib/zlib_inflate/inflate.o
  CC      fs/overlayfs/readdir.o
  CC      io_uring/openclose.o
  CC      lib/zlib_inflate/infutil.o
  CC      lib/zlib_inflate/inftrees.o
  CC      io_uring/sqpoll.o
  CC      lib/zlib_inflate/inflate_syms.o
  CC      fs/overlayfs/copy_up.o
  AR      lib/zlib_inflate/built-in.a
  CC      lib/zlib_deflate/deflate.o
  CC      kernel/sys.o
  CC      lib/zlib_deflate/deftree.o
  CC      io_uring/xattr.o
  CC      fs/overlayfs/export.o
  CC      lib/zlib_deflate/deflate_syms.o
  CC      io_uring/nop.o
  CC      fs/overlayfs/params.o
  AR      lib/zlib_deflate/built-in.a
  CC      lib/lz4/lz4_decompress.o
  CC      kernel/umh.o
  CC      io_uring/fs.o
  CC      fs/overlayfs/xattrs.o
  CC      kernel/workqueue.o
  CC      io_uring/splice.o
  AR      fs/overlayfs/built-in.a
  CC      fs/xfs/xfs_trace.o
  AR      lib/lz4/built-in.a
  CC      lib/xz/xz_dec_syms.o
  CC      io_uring/sync.o
  CC      lib/xz/xz_dec_stream.o
  CC      fs/xfs/libxfs/xfs_ag.o
  CC      io_uring/msg_ring.o
  CC      lib/xz/xz_dec_lzma2.o
  CC      lib/xz/xz_dec_bcj.o
  CC      io_uring/advise.o
  CC      fs/xfs/libxfs/xfs_alloc.o
  AR      lib/xz/built-in.a
  CC      lib/dim/dim.o
  CC      io_uring/epoll.o
  CC      lib/dim/net_dim.o
  CC      io_uring/statx.o
  CC      kernel/pid.o
  CC      lib/dim/rdma_dim.o
  CC      io_uring/timeout.o
  AR      lib/dim/built-in.a
  CC      lib/fonts/fonts.o
  CC      fs/xfs/libxfs/xfs_alloc_btree.o
  CC      lib/fonts/font_8x16.o
  CC      kernel/task_work.o
  AR      lib/fonts/built-in.a
  CC      lib/argv_split.o
  CC      io_uring/fdinfo.o
  CC      fs/xfs/libxfs/xfs_attr.o
  CC      lib/bug.o
  CC      kernel/extable.o
  CC      io_uring/cancel.o
  CC      lib/buildid.o
  CC      kernel/params.o
  CC      fs/xfs/libxfs/xfs_attr_leaf.o
  CC      lib/cmdline.o
  CC      io_uring/waitid.o
  CC      lib/cpumask.o
  CC      lib/ctype.o
  CC      lib/dec_and_lock.o
  CC      kernel/kthread.o
  CC      io_uring/register.o
  CC      lib/decompress.o
  CC      lib/decompress_inflate.o
  CC      lib/dump_stack.o
  CC      fs/xfs/libxfs/xfs_attr_remote.o
  CC      lib/earlycpio.o
  CC      kernel/sys_ni.o
  CC      lib/extable.o
  CC      io_uring/truncate.o
  CC      lib/fdt.o
  CC      kernel/nsproxy.o
  CC      fs/xfs/libxfs/xfs_bit.o
  CC      lib/fdt_addresses.o
  CC      lib/fdt_empty_tree.o
  CC      lib/fdt_ro.o
  CC      io_uring/memmap.o
  CC      fs/xfs/libxfs/xfs_bmap.o
  CC      lib/fdt_rw.o
  CC      kernel/notifier.o
  CC      lib/fdt_strerror.o
  CC      lib/fdt_sw.o
  CC      io_uring/io-wq.o
  CC      lib/fdt_wip.o
  CC      lib/flex_proportions.o
  CC      lib/idr.o
  CC      kernel/ksysfs.o
  CC      kernel/cred.o
  CC      lib/irq_regs.o
  CC      lib/is_single_threaded.o
  CC      io_uring/futex.o
  CC      lib/klist.o
  CC      lib/kobject.o
  CC      kernel/reboot.o
  CC      io_uring/napi.o
  CC      fs/xfs/libxfs/xfs_bmap_btree.o
  CC      lib/kobject_uevent.o
  CC      kernel/async.o
  CC      fs/xfs/libxfs/xfs_btree.o
  AR      io_uring/built-in.a
  AR      drivers/cache/built-in.a
  CC      drivers/irqchip/irqchip.o
  CC      kernel/range.o
  CC      kernel/smpboot.o
  CC      lib/logic_pio.o
  CC      drivers/irqchip/irq-gic.o
  CC      kernel/ucount.o
  CC      lib/maple_tree.o
  CC      kernel/regset.o
  CC      kernel/ksyms_common.o
  CC      drivers/irqchip/irq-gic-common.o
  CC      drivers/irqchip/irq-msi-lib.o
  CC      kernel/groups.o
  CC      fs/xfs/libxfs/xfs_btree_staging.o
  CC      drivers/irqchip/irq-gic-v2m.o
  CC      kernel/freezer.o
  CC      drivers/irqchip/irq-gic-v3.o
  CC      fs/xfs/libxfs/xfs_da_btree.o
  CC      kernel/stacktrace.o
  CC      kernel/smp.o
  CC      drivers/irqchip/irq-gic-v3-mbi.o
  CC      fs/xfs/libxfs/xfs_defer.o
  CC      kernel/kallsyms.o
  CC      lib/memcat_p.o
  CC      drivers/irqchip/irq-gic-v3-its.o
  CC      lib/nmi_backtrace.o
  CC      fs/xfs/libxfs/xfs_dir2.o
  CC      kernel/utsname.o
  CC      lib/objpool.o
  CC      kernel/user_namespace.o
  CC      lib/plist.o
  CC      lib/radix-tree.o
  CC      fs/xfs/libxfs/xfs_dir2_block.o
  CC      kernel/pid_namespace.o
  CC      lib/ratelimit.o
  CC      lib/rbtree.o
  CC      lib/seq_buf.o
  UPD     kernel/config_data
  CC      kernel/stop_machine.o
  CC      fs/xfs/libxfs/xfs_dir2_data.o
  CC      lib/siphash.o
  CC      drivers/irqchip/irq-gic-v4.o
  CC      kernel/audit.o
  CC      drivers/irqchip/irq-gic-v3-its-msi-parent.o
  CC      lib/string.o
  CC      fs/xfs/libxfs/xfs_dir2_leaf.o
  CC      lib/timerqueue.o
  CC      drivers/irqchip/irq-partition-percpu.o
  CC      lib/union_find.o
  CC      lib/vsprintf.o
  AR      drivers/irqchip/built-in.a
  AR      drivers/bus/mhi/built-in.a
  CC      drivers/bus/simple-pm-bus.o
  CC      fs/xfs/libxfs/xfs_dir2_node.o
  AR      drivers/bus/built-in.a
  AR      drivers/pwm/built-in.a
  AR      drivers/leds/blink/built-in.a
  AR      drivers/leds/simple/built-in.a
  AR      drivers/leds/built-in.a
  CC      drivers/pci/msi/pcidev_msi.o
  CC      kernel/auditfilter.o
  CC      drivers/pci/msi/api.o
  CC      drivers/pci/msi/msi.o
  CC      fs/xfs/libxfs/xfs_dir2_sf.o
  CC      kernel/auditsc.o
  CC      lib/win_minmax.o
  CC      lib/xarray.o
  CC      drivers/pci/msi/irqdomain.o
  CC      fs/xfs/libxfs/xfs_dquot_buf.o
  AR      drivers/pci/msi/built-in.a
  CC      drivers/pci/pcie/portdrv.o
  CC      lib/lockref.o
  CC      kernel/audit_watch.o
  CC      fs/xfs/libxfs/xfs_exchmaps.o
  CC      lib/bcd.o
  CC      lib/sort.o
  CC      lib/parser.o
  CC      drivers/pci/pcie/rcec.o
  CC      lib/debug_locks.o
  CC      lib/random32.o
  CC      kernel/audit_fsnotify.o
  CC      drivers/pci/pcie/aspm.o
  CC      lib/bust_spinlocks.o
  CC      fs/xfs/libxfs/xfs_ialloc.o
  CC      lib/kasprintf.o
  CC      kernel/audit_tree.o
  CC      lib/bitmap.o
  AR      drivers/pci/pcie/built-in.a
  AR      drivers/pci/pwrctl/built-in.a
  CC      drivers/pci/hotplug/pci_hotplug_core.o
  CC      lib/scatterlist.o
  CC      kernel/seccomp.o
  CC      fs/xfs/libxfs/xfs_ialloc_btree.o
  CC      drivers/pci/hotplug/acpi_pcihp.o
  CC      lib/list_sort.o
  CC      drivers/pci/hotplug/pciehp_core.o
  CC      lib/uuid.o
  CC      fs/xfs/libxfs/xfs_iext_tree.o
  CC      lib/iov_iter.o
  CC      drivers/pci/hotplug/pciehp_ctrl.o
  CC      kernel/utsname_sysctl.o
  CC      kernel/delayacct.o
  CC      fs/xfs/libxfs/xfs_inode_fork.o
  CC      drivers/pci/hotplug/pciehp_pci.o
  CC      kernel/taskstats.o
  CC      drivers/pci/hotplug/pciehp_hpc.o
  CC      lib/clz_ctz.o
  CC      lib/bsearch.o
  CC      fs/xfs/libxfs/xfs_inode_buf.o
  CC      kernel/tsacct.o
  CC      lib/find_bit.o
  CC      drivers/pci/hotplug/acpiphp_core.o
  CC      lib/llist.o
  CC      kernel/irq_work.o
  CC      lib/lwq.o
  CC      fs/xfs/libxfs/xfs_inode_util.o
  CC      lib/memweight.o
  CC      drivers/pci/hotplug/acpiphp_glue.o
  CC      lib/kfifo.o
  CC      kernel/cpu_pm.o
  CC      kernel/padata.o
  CC      fs/xfs/libxfs/xfs_log_rlimit.o
  CC      lib/percpu-refcount.o
  AR      drivers/pci/hotplug/built-in.a
  CC      drivers/pci/controller/dwc/pcie-al.o
  CC      drivers/pci/controller/dwc/pcie-hisi.o
  CC      kernel/context_tracking.o
  CC      lib/rhashtable.o
  CC      fs/xfs/libxfs/xfs_ag_resv.o
  CC      drivers/pci/controller/dwc/pcie-tegra194-acpi.o
  CC      kernel/iomem.o
  CC      fs/xfs/libxfs/xfs_parent.o
  CC      lib/base64.o
  AR      drivers/pci/controller/dwc/built-in.a
  AR      drivers/pci/controller/mobiveil/built-in.a
  AR      drivers/pci/controller/plda/built-in.a
  CC      drivers/pci/controller/pci-host-common.o
  CC      lib/once.o
  CC      kernel/rseq.o
  CC      lib/refcount.o
  CC      drivers/pci/controller/pci-host-generic.o
  CC      fs/xfs/libxfs/xfs_rmap.o
  CC      lib/rcuref.o
  GZIP    kernel/config_data.gz
  CC      kernel/configs.o
  CC      lib/usercopy.o
  CC      drivers/pci/controller/pci-thunder-ecam.o
  CC      lib/errseq.o
  AR      kernel/built-in.a
  CC      lib/bucket_locks.o
  CC      fs/9p/vfs_super.o
  CC      lib/generic-radix-tree.o
  CC      drivers/pci/controller/pci-thunder-pem.o
  CC      fs/9p/vfs_inode.o
  CC      lib/bitmap-str.o
  CC      fs/xfs/libxfs/xfs_rmap_btree.o
  CC      drivers/pci/controller/pci-xgene.o
  CC      lib/string_helpers.o
  AR      drivers/pci/controller/built-in.a
  CC      fs/9p/vfs_inode_dotl.o
  AR      drivers/pci/switch/built-in.a
  CC      drivers/pci/access.o
  CC      fs/xfs/libxfs/xfs_refcount.o
  CC      lib/hexdump.o
  CC      lib/kstrtox.o
  CC      fs/9p/vfs_addr.o
  CC      drivers/pci/bus.o
  CC      lib/iomap_copy.o
  CC      lib/devres.o
  CC      fs/xfs/libxfs/xfs_refcount_btree.o
  CC      fs/9p/vfs_file.o
  CC      drivers/pci/probe.o
  CC      lib/hweight.o
  CC      lib/interval_tree.o
  CC      lib/assoc_array.o
  CC      fs/xfs/libxfs/xfs_sb.o
  CC      fs/9p/vfs_dir.o
  CC      lib/bitrev.o
  CC      lib/crc16.o
  CC      fs/9p/vfs_dentry.o
  CC      drivers/pci/host-bridge.o
  HOSTCC  lib/gen_crc32table
  CC      lib/libcrc32c.o
  CC      fs/xfs/libxfs/xfs_symlink_remote.o
  CC      fs/9p/v9fs.o
  CC      drivers/pci/remove.o
  CC      lib/xxhash.o
  CC      drivers/pci/pci.o
  CC      fs/xfs/libxfs/xfs_trans_inode.o
  CC      lib/genalloc.o
  CC      fs/9p/fid.o
  CC      fs/xfs/libxfs/xfs_trans_resv.o
  CC      lib/textsearch.o
  CC      fs/9p/xattr.o
  CC      lib/ts_kmp.o
  CC      fs/xfs/libxfs/xfs_trans_space.o
  CC      fs/9p/acl.o
  CC      lib/ts_bm.o
  CC      lib/ts_fsm.o
  CC      fs/xfs/libxfs/xfs_types.o
  AR      fs/9p/built-in.a
  AR      fs/hostfs/built-in.a
  CC      lib/percpu_counter.o
  CC      drivers/video/console/dummycon.o
  CC      drivers/pci/pci-driver.o
  CC      lib/audit.o
  CC      fs/xfs/xfs_aops.o
  AR      drivers/video/console/built-in.a
  AR      drivers/video/backlight/built-in.a
  AR      drivers/video/fbdev/core/built-in.a
  AR      drivers/video/fbdev/omap/built-in.a
  AR      drivers/video/fbdev/omap2/omapfb/dss/built-in.a
  AR      drivers/video/fbdev/omap2/omapfb/displays/built-in.a
  AR      drivers/video/fbdev/omap2/omapfb/built-in.a
  AR      drivers/video/fbdev/omap2/built-in.a
  AR      drivers/video/fbdev/built-in.a
  AR      drivers/video/built-in.a
  AR      drivers/idle/built-in.a
  CC      lib/syscall.o
  AR      drivers/char/ipmi/built-in.a
  CC      fs/debugfs/inode.o
  CC      drivers/pci/search.o
  CC      lib/nlattr.o
  CC      fs/xfs/xfs_attr_inactive.o
  CC      drivers/pci/rom.o
  CC      fs/debugfs/file.o
  CC      fs/xfs/xfs_attr_list.o
  CC      lib/checksum.o
  CC      drivers/pci/setup-res.o
  CC      lib/cpu_rmap.o
  AR      fs/debugfs/built-in.a
  CC      drivers/pci/irq.o
  CC      lib/dynamic_queue_limits.o
  CC      drivers/pci/vpd.o
  CC      fs/xfs/xfs_bmap_util.o
  CC      drivers/pci/setup-bus.o
  CC      fs/xfs/xfs_bio_io.o
  CC      lib/strncpy_from_user.o
  CC      lib/strnlen_user.o
  CC      drivers/acpi/acpica/dsargs.o
  CC      fs/xfs/xfs_buf.o
  CC      lib/net_utils.o
  CC      drivers/acpi/acpica/dscontrol.o
  CC      drivers/acpi/acpica/dsdebug.o
  CC      drivers/pci/vc.o
  CC      lib/sg_pool.o
  CC      drivers/acpi/acpica/dsfield.o
  CC      drivers/acpi/acpica/dsinit.o
  CC      lib/memregion.o
  CC      drivers/pci/mmap.o
  CC      lib/stackdepot.o
  CC      drivers/acpi/acpica/dsmethod.o
  CC      fs/xfs/xfs_dahash_test.o
  CC      drivers/pci/devres.o
  CC      drivers/acpi/acpica/dsmthdat.o
  CC      lib/asn1_decoder.o
  CC      fs/xfs/xfs_dir2_readdir.o
  CC      drivers/acpi/acpica/dsobject.o
  CC      drivers/pci/proc.o
  CC      drivers/acpi/acpica/dsopcode.o
  CC      lib/ucs2_string.o
  CC      drivers/acpi/acpica/dspkginit.o
  CC      lib/sbitmap.o
  CC      fs/xfs/xfs_discard.o
  CC      drivers/pci/pci-sysfs.o
  CC      drivers/acpi/acpica/dsutils.o
  CC      drivers/acpi/acpica/dswexec.o
  CC      lib/group_cpus.o
  CC      fs/xfs/xfs_error.o
  CC      drivers/acpi/acpica/dswload.o
  CC      drivers/pci/slot.o
  CC      lib/devmem_is_allowed.o
  CC      drivers/acpi/acpica/dswload2.o
  CC      fs/xfs/xfs_exchrange.o
  CC      drivers/acpi/acpica/dswscope.o
  CC      lib/fw_table.o
  CC      drivers/pci/pci-acpi.o
  CC      drivers/acpi/acpica/dswstate.o
  AR      lib/lib.a
  GEN     lib/crc32table.h
  CC      lib/crc32.o
  CC      drivers/acpi/acpica/evevent.o
  CC      drivers/acpi/acpica/evgpe.o
  CC      fs/xfs/xfs_export.o
  AR      lib/built-in.a
  CC      drivers/pci/iomap.o
  CC      drivers/acpi/acpica/evgpeblk.o
  AR      sound/built-in.a
  CC      drivers/pci/of.o
  CC      drivers/acpi/acpica/evgpeinit.o
  CC      fs/xfs/xfs_extent_busy.o
  CC      drivers/pci/quirks.o
  CC      drivers/acpi/acpica/evgpeutil.o
  CC      drivers/acpi/acpica/evglock.o
  CC      drivers/acpi/nfit/core.o
  CC      drivers/acpi/acpica/evhandler.o
  CC      fs/xfs/xfs_file.o
  CC      drivers/acpi/acpica/evmisc.o
  CC      drivers/acpi/acpica/evregion.o
  CC      drivers/acpi/acpica/evrgnini.o
  CC      drivers/pci/pci-label.o
  CC      drivers/acpi/acpica/evsci.o
  CC      fs/xfs/xfs_filestream.o
  CC      drivers/acpi/acpica/evxface.o
  CC      drivers/pci/syscall.o
  CC      drivers/acpi/nfit/intel.o
  CC      drivers/acpi/acpica/evxfevnt.o
  CC      drivers/acpi/acpica/evxfgpe.o
  CC      fs/xfs/xfs_fsmap.o
  CC      drivers/pci/ecam.o
  AR      drivers/acpi/nfit/built-in.a
  CC      drivers/pnp/pnpacpi/core.o
  CC      drivers/acpi/acpica/evxfregn.o
  CC      drivers/acpi/acpica/exconcat.o
  AR      drivers/pci/built-in.a
  CC      drivers/amba/bus.o
  CC      drivers/pnp/pnpacpi/rsparser.o
  CC      drivers/acpi/acpica/exconfig.o
  CC      fs/xfs/xfs_fsops.o
  CC      drivers/acpi/acpica/exconvrt.o
  AR      drivers/amba/built-in.a
  AR      drivers/clk/actions/built-in.a
  AR      drivers/clk/analogbits/built-in.a
  AR      drivers/clk/bcm/built-in.a
  AR      drivers/clk/imgtec/built-in.a
  AR      drivers/clk/imx/built-in.a
  AR      drivers/clk/ingenic/built-in.a
  AR      drivers/clk/mediatek/built-in.a
  AR      drivers/pnp/pnpacpi/built-in.a
  AR      drivers/clk/microchip/built-in.a
  CC      drivers/pnp/core.o
  AR      drivers/clk/mstar/built-in.a
  AR      drivers/clk/mvebu/built-in.a
  CC      drivers/acpi/acpica/excreate.o
  AR      drivers/clk/ralink/built-in.a
  AR      drivers/clk/renesas/built-in.a
  AR      drivers/clk/socfpga/built-in.a
  AR      drivers/clk/sophgo/built-in.a
  AR      drivers/clk/sprd/built-in.a
  AR      drivers/clk/starfive/built-in.a
  AR      drivers/clk/sunxi-ng/built-in.a
  AR      drivers/clk/ti/built-in.a
  AR      drivers/clk/versatile/built-in.a
  AR      drivers/clk/xilinx/built-in.a
  CC      drivers/clk/clk-devres.o
  CC      fs/xfs/xfs_globals.o
  CC      drivers/acpi/acpica/exdebug.o
  CC      drivers/pnp/card.o
  CC      drivers/clk/clk-bulk.o
  CC      drivers/acpi/acpica/exdump.o
  CC      fs/xfs/xfs_handle.o
  CC      drivers/acpi/acpica/exfield.o
  CC      drivers/clk/clkdev.o
  CC      drivers/pnp/driver.o
  CC      drivers/acpi/acpica/exfldio.o
  CC      drivers/clk/clk.o
  CC      drivers/pnp/resource.o
  CC      drivers/acpi/acpica/exmisc.o
  CC      fs/xfs/xfs_health.o
  CC      drivers/acpi/acpica/exmutex.o
  CC      drivers/acpi/acpica/exnames.o
  CC      drivers/pnp/manager.o
  CC      drivers/acpi/acpica/exoparg1.o
  CC      fs/xfs/xfs_icache.o
  CC      drivers/acpi/acpica/exoparg2.o
  CC      drivers/pnp/support.o
  CC      drivers/acpi/acpica/exoparg3.o
  CC      drivers/pnp/interface.o
  CC      drivers/clk/clk-divider.o
  CC      drivers/acpi/acpica/exoparg6.o
  CC      drivers/acpi/acpica/exprep.o
  CC      drivers/pnp/quirks.o
  CC      drivers/acpi/acpica/exregion.o
  CC      drivers/clk/clk-fixed-factor.o
  CC      fs/xfs/xfs_ioctl.o
  CC      drivers/acpi/acpica/exresnte.o
  CC      drivers/pnp/system.o
  CC      drivers/clk/clk-fixed-rate.o
  CC      drivers/acpi/acpica/exresolv.o
  AR      drivers/pnp/built-in.a
  AR      drivers/soc/apple/built-in.a
  AR      drivers/soc/aspeed/built-in.a
  AR      drivers/soc/bcm/built-in.a
  AR      drivers/soc/fsl/built-in.a
  AR      drivers/soc/fujitsu/built-in.a
  AR      drivers/soc/hisilicon/built-in.a
  AR      drivers/soc/imx/built-in.a
  AR      drivers/soc/ixp4xx/built-in.a
  AR      drivers/soc/loongson/built-in.a
  AR      drivers/soc/mediatek/built-in.a
  AR      drivers/soc/microchip/built-in.a
  AR      drivers/soc/nuvoton/built-in.a
  AR      drivers/soc/pxa/built-in.a
  AR      drivers/soc/amlogic/built-in.a
  AR      drivers/soc/qcom/built-in.a
  AR      drivers/soc/renesas/built-in.a
  AR      drivers/soc/rockchip/built-in.a
  CC      drivers/acpi/acpica/exresop.o
  AR      drivers/soc/sunxi/built-in.a
  AR      drivers/soc/ti/built-in.a
  AR      drivers/soc/versatile/built-in.a
  AR      drivers/soc/xilinx/built-in.a
  AR      drivers/soc/built-in.a
  CC      drivers/clk/clk-gate.o
  CC      drivers/clk/clk-multiplier.o
  CC      fs/xfs/xfs_iomap.o
  CC      drivers/acpi/acpica/exserial.o
  CC      drivers/acpi/acpica/exstore.o
  CC      fs/erofs/super.o
  CC      drivers/clk/clk-mux.o
  CC      drivers/acpi/acpica/exstoren.o
  CC      drivers/acpi/acpica/exstorob.o
  CC      drivers/clk/clk-composite.o
  CC      fs/xfs/xfs_iops.o
  CC      drivers/acpi/acpica/exsystem.o
  CC      fs/erofs/inode.o
  CC      drivers/clk/clk-fractional-divider.o
  CC      drivers/acpi/acpica/extrace.o
  CC      drivers/acpi/acpica/exutils.o
  CC      fs/erofs/data.o
  CC      drivers/clk/clk-gpio.o
  CC      drivers/acpi/acpica/hwacpi.o
  CC      fs/xfs/xfs_inode.o
  CC      drivers/acpi/acpica/hwesleep.o
  CC      drivers/clk/clk-conf.o
  CC      fs/erofs/namei.o
  CC      drivers/acpi/acpica/hwgpe.o
  AR      drivers/clk/built-in.a
  CC      drivers/virtio/virtio.o
  CC      drivers/acpi/acpica/hwregs.o
  CC      drivers/acpi/acpica/hwsleep.o
  CC      fs/erofs/dir.o
  CC      drivers/acpi/acpica/hwvalid.o
  CC      drivers/virtio/virtio_ring.o
  CC      drivers/acpi/acpica/hwxface.o
  CC      fs/erofs/sysfs.o
  CC      fs/xfs/xfs_itable.o
  CC      drivers/acpi/acpica/hwxfsleep.o
  CC      fs/erofs/xattr.o
  CC      drivers/acpi/acpica/hwpci.o
  CC      fs/xfs/xfs_iwalk.o
  CC      drivers/acpi/acpica/nsaccess.o
  CC      drivers/virtio/virtio_anchor.o
  CC      drivers/acpi/acpica/nsalloc.o
  CC      fs/erofs/decompressor.o
  CC      drivers/virtio/virtio_pci_modern_dev.o
  CC      drivers/acpi/acpica/nsarguments.o
  CC      fs/xfs/xfs_message.o
  CC      drivers/acpi/acpica/nsconvert.o
  CC      fs/erofs/zmap.o
  CC      drivers/virtio/virtio_pci_legacy_dev.o
  CC      drivers/acpi/acpica/nsdump.o
  CC      fs/xfs/xfs_mount.o
  CC      drivers/acpi/acpica/nseval.o
  CC      drivers/virtio/virtio_mmio.o
  CC      drivers/acpi/acpica/nsinit.o
  CC      fs/erofs/zdata.o
  CC      drivers/acpi/acpica/nsload.o
  CC      fs/xfs/xfs_mru_cache.o
  CC      drivers/acpi/acpica/nsnames.o
  CC      drivers/virtio/virtio_pci_modern.o
  CC      drivers/acpi/acpica/nsobject.o
  CC      fs/xfs/xfs_pwork.o
  CC      drivers/acpi/acpica/nsparse.o
  CC      drivers/virtio/virtio_pci_common.o
  CC      drivers/acpi/acpica/nspredef.o
  CC      fs/erofs/zutil.o
  CC      drivers/acpi/acpica/nsprepkg.o
  CC      fs/xfs/xfs_reflink.o
  CC      drivers/acpi/acpica/nsrepair.o
  AR      fs/erofs/built-in.a
  CC      drivers/tty/vt/vt_ioctl.o
  CC      drivers/virtio/virtio_pci_legacy.o
  CC      drivers/acpi/acpica/nsrepair2.o
  CC      drivers/virtio/virtio_balloon.o
  CC      drivers/acpi/acpica/nssearch.o
  CC      fs/xfs/xfs_stats.o
  CC      drivers/acpi/acpica/nsutils.o
  CC      drivers/tty/vt/vc_screen.o
  CC      drivers/acpi/acpica/nswalk.o
  CC      fs/xfs/xfs_super.o
  CC      drivers/acpi/acpica/nsxfeval.o
  CC      drivers/virtio/virtio_mem.o
  CC      drivers/tty/vt/selection.o
  CC      drivers/acpi/acpica/nsxfname.o
  CC      drivers/acpi/acpica/nsxfobj.o
  CC      drivers/tty/vt/keyboard.o
  CC      drivers/acpi/acpica/psargs.o
  CC      fs/xfs/xfs_symlink.o
  CC      drivers/acpi/acpica/psloop.o
  AR      drivers/virtio/built-in.a
  CC      drivers/tty/hvc/hvc_console.o
  CC      drivers/acpi/acpica/psobject.o
  CC      fs/xfs/xfs_sysfs.o
  CC      drivers/acpi/acpica/psopcode.o
  CC      drivers/tty/vt/vt.o
  CC      drivers/acpi/acpica/psopinfo.o
  AR      drivers/tty/hvc/built-in.a
  CC      drivers/acpi/numa/srat.o
  CC      fs/xfs/xfs_trans.o
  CC      drivers/acpi/acpica/psparse.o
  CC      drivers/acpi/acpica/psscope.o
  AR      drivers/acpi/numa/built-in.a
  CC      net/core/sock.o
  CC      drivers/acpi/acpica/pstree.o
  CC      drivers/acpi/acpica/psutils.o
  CC      fs/xfs/xfs_xattr.o
  CC      drivers/acpi/acpica/pswalk.o
  CC      drivers/acpi/acpica/psxface.o
  CC      fs/xfs/xfs_log.o
  CC      drivers/acpi/acpica/rsaddr.o
  COPY    drivers/tty/vt/defkeymap.c
  CC      drivers/tty/vt/consolemap.o
  CC      drivers/acpi/acpica/rscalc.o
  CC      drivers/acpi/acpica/rscreate.o
  HOSTCC  drivers/tty/vt/conmakehash
  CC      drivers/tty/vt/defkeymap.o
  CC      drivers/acpi/acpica/rsdumpinfo.o
  CONMK   drivers/tty/vt/consolemap_deftbl.c
  CC      drivers/tty/vt/consolemap_deftbl.o
  AR      drivers/tty/vt/built-in.a
  CC      drivers/tty/serial/8250/8250_core.o
  CC      drivers/acpi/acpica/rsinfo.o
  CC      drivers/acpi/acpica/rsio.o
  CC      fs/xfs/xfs_log_cil.o
  CC      net/core/request_sock.o
  CC      drivers/acpi/acpica/rsirq.o
  CC      drivers/acpi/acpica/rslist.o
  CC      drivers/tty/serial/8250/8250_platform.o
  CC      drivers/acpi/acpica/rsmemory.o
  CC      net/core/skbuff.o
  CC      drivers/acpi/acpica/rsmisc.o
  CC      fs/xfs/xfs_bmap_item.o
  CC      drivers/tty/serial/8250/8250_port.o
  CC      drivers/acpi/acpica/rsserial.o
  CC      drivers/acpi/acpica/rsutils.o
  CC      fs/xfs/xfs_buf_item.o
  CC      drivers/acpi/acpica/rsxface.o
  CC      drivers/acpi/acpica/tbdata.o
  CC      drivers/tty/serial/8250/8250_pcilib.o
  CC      drivers/acpi/acpica/tbfadt.o
  CC      fs/xfs/xfs_buf_item_recover.o
  CC      drivers/acpi/acpica/tbfind.o
  CC      drivers/tty/serial/8250/8250_early.o
  CC      drivers/acpi/acpica/tbinstal.o
  CC      drivers/acpi/acpica/tbprint.o
  CC      fs/xfs/xfs_dquot_item_recover.o
  CC      drivers/tty/serial/8250/8250_fsl.o
  CC      drivers/acpi/acpica/tbutils.o
  CC      drivers/acpi/acpica/tbxface.o
  CC      fs/xfs/xfs_exchmaps_item.o
  CC      drivers/tty/serial/8250/8250_of.o
  CC      drivers/acpi/acpica/tbxfload.o
  CC      drivers/tty/serial/8250/8250_pci.o
  CC      drivers/acpi/acpica/tbxfroot.o
  CC      fs/xfs/xfs_extfree_item.o
  CC      net/core/datagram.o
  CC      drivers/acpi/acpica/utaddress.o
  CC      drivers/acpi/acpica/utalloc.o
  CC      drivers/acpi/acpica/utascii.o
  CC      fs/xfs/xfs_attr_item.o
  CC      drivers/acpi/acpica/utbuffer.o
  AR      drivers/tty/serial/8250/built-in.a
  CC      drivers/tty/serial/serial_core.o
  CC      drivers/acpi/acpica/utcksum.o
  CC      net/core/stream.o
  CC      drivers/acpi/acpica/utcopy.o
  CC      drivers/acpi/acpica/utexcep.o
  CC      fs/xfs/xfs_icreate_item.o
  CC      drivers/acpi/acpica/utdebug.o
  CC      net/core/scm.o
  CC      drivers/acpi/acpica/utdecode.o
  CC      fs/xfs/xfs_inode_item.o
  CC      drivers/acpi/acpica/utdelete.o
  CC      drivers/acpi/acpica/uterror.o
  CC      drivers/tty/serial/serial_base_bus.o
  CC      net/core/gen_stats.o
  CC      drivers/acpi/acpica/uteval.o
  CC      drivers/tty/serial/serial_ctrl.o
  CC      drivers/acpi/acpica/utglobal.o
  CC      fs/xfs/xfs_inode_item_recover.o
  CC      drivers/acpi/acpica/uthex.o
  CC      drivers/tty/serial/serial_port.o
  CC      net/core/gen_estimator.o
  CC      drivers/acpi/acpica/utids.o
  CC      drivers/tty/serial/earlycon.o
  CC      fs/xfs/xfs_iunlink_item.o
  CC      drivers/acpi/acpica/utinit.o
  CC      drivers/acpi/acpica/utlock.o
  CC      drivers/tty/serial/amba-pl011.o
  CC      net/core/net_namespace.o
  CC      drivers/acpi/acpica/utmath.o
  CC      fs/xfs/xfs_refcount_item.o
  CC      drivers/acpi/acpica/utmisc.o
  CC      drivers/acpi/acpica/utmutex.o
  CC      drivers/acpi/acpica/utnonansi.o
  CC      fs/xfs/xfs_rmap_item.o
  CC      drivers/acpi/acpica/utobject.o
  CC      net/core/secure_seq.o
  AR      drivers/tty/serial/built-in.a
  AR      drivers/tty/ipwireless/built-in.a
  CC      drivers/tty/tty_io.o
  CC      drivers/acpi/acpica/utosi.o
  CC      fs/xfs/xfs_log_recover.o
  CC      drivers/acpi/acpica/utownerid.o
  CC      drivers/acpi/acpica/utpredef.o
  CC      net/core/flow_dissector.o
  CC      drivers/acpi/acpica/utresdecode.o
  CC      drivers/acpi/acpica/utresrc.o
  CC      drivers/acpi/acpica/utstate.o
  CC      drivers/tty/n_tty.o
  CC      drivers/acpi/acpica/utstring.o
  CC      fs/xfs/xfs_trans_ail.o
  CC      drivers/acpi/acpica/utstrsuppt.o
  CC      drivers/acpi/acpica/utstrtoul64.o
  CC      net/core/sysctl_net_core.o
  CC      drivers/acpi/acpica/utxface.o
  CC      drivers/tty/tty_ioctl.o
  CC      fs/xfs/xfs_trans_buf.o
  CC      drivers/acpi/acpica/utxfinit.o
  CC      drivers/acpi/acpica/utxferror.o
  CC      drivers/tty/tty_ldisc.o
  CC      net/core/dev.o
  CC      drivers/acpi/acpica/utxfmutex.o
  CC      fs/xfs/xfs_sysctl.o
  AR      drivers/acpi/acpica/built-in.a
  AR      drivers/acpi/pmic/built-in.a
  CC      drivers/acpi/dptf/int340x_thermal.o
  CC      fs/xfs/xfs_pnfs.o
  CC      drivers/tty/tty_buffer.o
  AR      drivers/acpi/dptf/built-in.a
  CC      drivers/acpi/arm64/apmt.o
  CC      drivers/tty/tty_port.o
  CC      drivers/acpi/arm64/gtdt.o
  AR      fs/xfs/built-in.a
  CC      fs/open.o
  CC      drivers/acpi/arm64/iort.o
  CC      drivers/tty/tty_mutex.o
  CC      drivers/tty/tty_ldsem.o
  CC      fs/read_write.o
  CC      drivers/tty/tty_baudrate.o
  CC      drivers/acpi/arm64/cpuidle.o
  CC      drivers/tty/tty_jobctrl.o
  CC      drivers/acpi/arm64/amba.o
  CC      drivers/tty/n_null.o
  CC      drivers/acpi/arm64/dma.o
  CC      fs/file_table.o
  CC      drivers/tty/pty.o
  CC      drivers/acpi/arm64/init.o
  CC      fs/super.o
  CC      drivers/tty/tty_audit.o
  CC      drivers/acpi/arm64/thermal_cpufreq.o
  AR      drivers/tty/built-in.a
  AR      drivers/acpi/arm64/built-in.a
  CC      drivers/acpi/tables.o
  CC      virt/lib/irqbypass.o
  CC      fs/char_dev.o
  CC      net/core/dev_addr_lists.o
  AR      virt/lib/built-in.a
  AR      virt/built-in.a
  CC      net/llc/llc_core.o
  CC      drivers/acpi/osi.o
  CC      fs/stat.o
  CC      drivers/acpi/osl.o
  CC      net/llc/llc_input.o
  CC      net/core/dst.o
  CC      fs/exec.o
  CC      net/llc/llc_output.o
  CC      drivers/acpi/utils.o
  CC      net/core/netevent.o
  AR      net/llc/built-in.a
  CC      net/core/neighbour.o
  CC      drivers/acpi/reboot.o
  CC      net/core/rtnetlink.o
  CC      fs/pipe.o
  CC      drivers/acpi/nvs.o
  CC      drivers/acpi/wakeup.o
  CC      drivers/acpi/device_sysfs.o
  CC      fs/namei.o
  CC      drivers/acpi/device_pm.o
  CC      drivers/char/hw_random/core.o
  CC      drivers/acpi/bus.o
  CC      drivers/char/hw_random/virtio-rng.o
  CC      net/core/utils.o
  CC      drivers/acpi/glue.o
  AR      drivers/char/hw_random/built-in.a
  AR      drivers/char/agp/built-in.a
  CC      drivers/char/mem.o
  CC      drivers/acpi/scan.o
  CC      fs/fcntl.o
  CC      drivers/char/random.o
  CC      net/core/link_watch.o
  CC      fs/ioctl.o
  CC      net/core/filter.o
  CC      drivers/acpi/mipi-disco-img.o
  CC      drivers/char/misc.o
  CC      drivers/char/virtio_console.o
  CC      fs/readdir.o
  CC      drivers/acpi/resource.o
  CC      fs/select.o
  CC      drivers/acpi/acpi_processor.o
  AR      drivers/char/built-in.a
  AR      drivers/iommu/amd/built-in.a
  AR      drivers/iommu/intel/built-in.a
  AR      drivers/iommu/arm/arm-smmu/built-in.a
  AR      drivers/iommu/arm/arm-smmu-v3/built-in.a
  AR      drivers/iommu/arm/built-in.a
  AR      drivers/iommu/iommufd/built-in.a
  CC      drivers/iommu/iommu.o
  CC      drivers/acpi/processor_core.o
  CC      fs/dcache.o
  CC      drivers/acpi/ec.o
  CC      drivers/iommu/iommu-traces.o
  CC      drivers/acpi/pci_root.o
  CC      drivers/iommu/iommu-sysfs.o
  CC      drivers/iommu/dma-iommu.o
  CC      fs/inode.o
  CC      drivers/acpi/pci_link.o
  CC      drivers/acpi/pci_irq.o
  CC      net/core/sock_diag.o
  CC      drivers/iommu/iova.o
  CC      drivers/acpi/acpi_apd.o
  CC      fs/attr.o
  CC      net/core/dev_ioctl.o
  CC      drivers/acpi/acpi_platform.o
  CC      drivers/iommu/of_iommu.o
  CC      fs/bad_inode.o
  CC      drivers/acpi/acpi_pnp.o
  AR      drivers/iommu/built-in.a
  AR      drivers/gpu/host1x/built-in.a
  CC      fs/file.o
  AR      drivers/gpu/drm/tests/built-in.a
  AR      drivers/gpu/drm/arm/built-in.a
  AR      drivers/gpu/drm/display/built-in.a
  AR      drivers/gpu/drm/renesas/rcar-du/built-in.a
  AR      drivers/gpu/drm/renesas/rz-du/built-in.a
  AR      drivers/gpu/drm/renesas/built-in.a
  AR      drivers/gpu/drm/omapdrm/built-in.a
  AR      drivers/gpu/drm/tilcdc/built-in.a
  AR      drivers/gpu/drm/imx/built-in.a
  AR      drivers/gpu/drm/i2c/built-in.a
  AR      drivers/gpu/drm/panel/built-in.a
  CC      net/core/tso.o
  AR      drivers/gpu/drm/bridge/analogix/built-in.a
  AR      drivers/gpu/drm/bridge/cadence/built-in.a
  AR      drivers/gpu/drm/bridge/imx/built-in.a
  AR      drivers/gpu/drm/bridge/synopsys/built-in.a
  AR      drivers/gpu/drm/bridge/built-in.a
  AR      drivers/gpu/drm/hisilicon/built-in.a
  AR      drivers/gpu/drm/mxsfb/built-in.a
  AR      drivers/gpu/drm/tiny/built-in.a
  AR      drivers/gpu/drm/xlnx/built-in.a
  CC      drivers/acpi/power.o
  AR      drivers/gpu/drm/gud/built-in.a
  AR      drivers/gpu/drm/solomon/built-in.a
  AR      drivers/gpu/drm/built-in.a
  AR      drivers/gpu/vga/built-in.a
  AR      drivers/gpu/built-in.a
  CC      net/core/sock_reuseport.o
  CC      drivers/acpi/event.o
  CC      net/core/fib_notifier.o
  CC      fs/filesystems.o
  CC      net/ethernet/eth.o
  CC      drivers/acpi/evged.o
  CC      net/core/xdp.o
  CC      fs/namespace.o
  CC      drivers/acpi/sysfs.o
  AR      net/ethernet/built-in.a
  CC      drivers/base/power/clock_ops.o
  CC      drivers/acpi/property.o
  CC      net/core/flow_offload.o
  AR      drivers/base/power/built-in.a
  CC      drivers/base/firmware_loader/builtin/main.o
  AR      drivers/base/firmware_loader/builtin/built-in.a
  CC      drivers/base/firmware_loader/main.o
  CC      drivers/acpi/debugfs.o
  CC      net/core/gro.o
  AR      drivers/base/firmware_loader/built-in.a
  AR      drivers/base/test/built-in.a
  CC      drivers/base/component.o
  CC      drivers/acpi/acpi_lpat.o
  CC      drivers/base/core.o
  CC      drivers/acpi/irq.o
  CC      net/core/netdev-genl.o
  CC      fs/seq_file.o
  CC      drivers/acpi/pci_mcfg.o
  CC      drivers/acpi/button.o
  CC      fs/xattr.o
  CC      net/core/netdev-genl-gen.o
  CC      drivers/acpi/pci_slot.o
  CC      drivers/base/bus.o
  CC      fs/libfs.o
  CC      net/core/gso.o
  CC      drivers/acpi/processor_driver.o
  CC      drivers/acpi/processor_thermal.o
  CC      drivers/base/dd.o
  CC      net/core/net-sysfs.o
  CC      drivers/acpi/processor_idle.o
  CC      fs/fs-writeback.o
  CC      drivers/base/syscore.o
  CC      drivers/acpi/processor_perflib.o
  CC      drivers/base/driver.o
  CC      drivers/base/class.o
  CC      net/core/hotdata.o
  CC      drivers/acpi/container.o
  CC      fs/pnode.o
  CC      drivers/base/platform.o
  CC      drivers/acpi/acpi_memhotplug.o
  CC      net/core/netdev_rx_queue.o
  CC      fs/splice.o
  CC      drivers/acpi/spcr.o
  CC      net/core/page_pool.o
  CC      drivers/base/cpu.o
  CC      drivers/acpi/pptt.o
  CC      drivers/base/firmware.o
  CC      fs/sync.o
  AR      drivers/acpi/built-in.a
  CC      net/802/p8022.o
  CC      drivers/base/init.o
  CC      net/core/page_pool_user.o
  CC      fs/utimes.o
  CC      drivers/base/map.o
  CC      net/802/psnap.o
  CC      drivers/base/devres.o
  CC      fs/d_path.o
  CC      net/core/net-procfs.o
  CC      net/802/stp.o
  CC      drivers/base/attribute_container.o
  CC      fs/stack.o
  AR      net/802/built-in.a
  CC      net/core/fib_rules.o
  CC      net/sched/sch_generic.o
  CC      drivers/base/transport_class.o
  CC      fs/fs_struct.o
  CC      drivers/base/topology.o
  CC      fs/statfs.o
  CC      drivers/base/container.o
  CC      fs/fs_pin.o
  CC      net/core/ptp_classifier.o
  CC      drivers/base/property.o
  CC      net/sched/sch_mq.o
  CC      fs/nsfs.o
  CC      net/core/netprio_cgroup.o
  CC      fs/fs_types.o
  CC      drivers/base/cacheinfo.o
  CC      net/sched/sch_frag.o
  CC      fs/fs_context.o
  CC      net/core/netclassid_cgroup.o
  CC      drivers/base/swnode.o
  CC      net/sched/sch_api.o
  CC      fs/fs_parser.o
  CC      net/core/dst_cache.o
  CC      drivers/base/devtmpfs.o
  CC      fs/fsopen.o
  CC      net/core/gro_cells.o
  CC      drivers/base/node.o
  CC      fs/init.o
  CC      net/sched/sch_blackhole.o
  CC      net/core/failover.o
  CC      drivers/base/memory.o
  CC      fs/kernel_read_file.o
  CC      net/sched/cls_api.o
  CC      fs/mnt_idmapping.o
  CC      net/core/skmsg.o
  CC      drivers/base/platform-msi.o
  CC      fs/remap_range.o
  CC      drivers/base/arch_topology.o
  CC      fs/pidfs.o
  CC      drivers/base/arch_numa.o
  CC      net/core/sock_map.o
  CC      net/sched/sch_fifo.o
  CC      fs/buffer.o
  CC      drivers/base/physical_location.o
  AR      drivers/base/built-in.a
  CC      drivers/block/brd.o
  CC      net/sched/sch_multiq.o
  CC      drivers/block/loop.o
  CC      net/core/bpf_sk_storage.o
  CC      net/sched/sch_fq_codel.o
  CC      fs/mpage.o
  CC      drivers/block/virtio_blk.o
  CC      net/core/of_net.o
  CC      fs/proc_namespace.o
  CC      net/sched/sch_fq.o
  AR      net/core/built-in.a
  CC      net/netlink/af_netlink.o
  CC      fs/eventpoll.o
  AR      drivers/block/built-in.a
  AR      drivers/misc/eeprom/built-in.a
  AR      drivers/misc/cb710/built-in.a
  AR      drivers/misc/ti-st/built-in.a
  AR      drivers/misc/lis3lv02d/built-in.a
  AR      drivers/misc/cardreader/built-in.a
  AR      drivers/misc/keba/built-in.a
  AR      drivers/misc/built-in.a
  AR      drivers/mfd/built-in.a
  AR      drivers/nfc/built-in.a
  CC      drivers/nvdimm/core.o
  CC      net/sched/cls_cgroup.o
  CC      drivers/nvdimm/bus.o
  CC      fs/anon_inodes.o
  CC      net/sched/ematch.o
  CC      net/netlink/genetlink.o
  CC      drivers/nvdimm/dimm_devs.o
  CC      fs/signalfd.o
  AR      net/sched/built-in.a
  CC      net/bpf/test_run.o
  CC      drivers/nvdimm/nd_perf.o
  CC      fs/timerfd.o
  CC      net/netlink/policy.o
  CC      drivers/nvdimm/dimm.o
  CC      fs/eventfd.o
  AR      net/netlink/built-in.a
  CC      fs/aio.o
  CC      drivers/nvdimm/region_devs.o
  AR      net/bpf/built-in.a
  CC      net/ethtool/ioctl.o
  CC      net/netfilter/ipset/ip_set_core.o
  CC      drivers/nvdimm/region.o
  CC      fs/dax.o
  CC      drivers/nvdimm/namespace_devs.o
  CC      net/netfilter/ipset/ip_set_getport.o
  CC      net/ethtool/common.o
  CC      fs/locks.o
  CC      net/netfilter/ipset/pfxlen.o
  CC      drivers/nvdimm/label.o
  AR      net/ethtool/built-in.a
  CC      net/ipv4/netfilter/nf_defrag_ipv4.o
  CC      net/netfilter/ipset/ip_set_bitmap_ip.o
  CC      drivers/nvdimm/badrange.o
  CC      net/ipv4/netfilter/nf_socket_ipv4.o
  CC      fs/binfmt_misc.o
  CC      drivers/nvdimm/claim.o
  CC      net/netfilter/ipset/ip_set_bitmap_ipmac.o
  CC      fs/binfmt_script.o
  CC      net/ipv4/netfilter/nf_tproxy_ipv4.o
  CC      drivers/nvdimm/btt_devs.o
  CC      fs/binfmt_elf.o
  CC      net/netfilter/ipset/ip_set_bitmap_port.o
  CC      net/ipv4/netfilter/nf_reject_ipv4.o
  CC      drivers/nvdimm/pfn_devs.o
  CC      fs/backing-file.o
  CC      drivers/nvdimm/dax_devs.o
  CC      net/netfilter/ipset/ip_set_hash_ip.o
  CC      net/ipv4/netfilter/nf_nat_h323.o
  CC      fs/mbcache.o
  CC      drivers/nvdimm/pmem.o
  CC      fs/posix_acl.o
  CC      net/ipv4/netfilter/nf_nat_pptp.o
  CC      drivers/nvdimm/btt.o
  CC      fs/coredump.o
  ASN.1   net/ipv4/netfilter/nf_nat_snmp_basic.asn1.[ch]
  CC      net/ipv4/netfilter/nft_reject_ipv4.o
  CC      net/netfilter/ipset/ip_set_hash_ipmark.o
  CC      drivers/nvdimm/of_pmem.o
  CC      net/ipv4/netfilter/nft_fib_ipv4.o
  CC      fs/drop_caches.o
  CC      drivers/nvdimm/virtio_pmem.o
  CC      fs/sysctls.o
  CC      fs/fhandle.o
  CC      drivers/nvdimm/nd_virtio.o
  CC      net/ipv4/netfilter/nft_dup_ipv4.o
  AR      drivers/nvdimm/built-in.a
  AR      fs/built-in.a
  CC      net/ipv4/netfilter/ip_tables.o
  CC      net/netfilter/ipset/ip_set_hash_ipport.o
  AR      drivers/dax/hmem/built-in.a
  CC      drivers/dax/super.o
  CC      net/xfrm/xfrm_policy.o
  CC      drivers/dax/bus.o
  CC      net/ipv4/netfilter/iptable_filter.o
  AR      drivers/dax/built-in.a
  AR      drivers/cxl/core/built-in.a
  AR      drivers/cxl/built-in.a
  AR      drivers/macintosh/built-in.a
  CC      drivers/scsi/scsi.o
  CC      net/ipv4/netfilter/iptable_mangle.o
  CC      net/netfilter/ipset/ip_set_hash_ipportip.o
  CC      drivers/scsi/hosts.o
  CC      net/ipv4/netfilter/iptable_nat.o
  CC      net/xfrm/xfrm_state.o
  CC      drivers/scsi/scsi_ioctl.o
  CC      net/ipv4/netfilter/iptable_raw.o
  CC      drivers/scsi/scsicam.o
  CC      net/netfilter/ipset/ip_set_hash_ipportnet.o
  CC      drivers/scsi/scsi_error.o
  CC      net/ipv4/netfilter/iptable_security.o
  CC      net/ipv4/netfilter/ipt_ah.o
  CC      drivers/scsi/scsi_lib.o
  CC      net/ipv4/netfilter/ipt_rpfilter.o
  CC      net/xfrm/xfrm_hash.o
  CC      net/xfrm/xfrm_input.o
  CC      net/ipv4/netfilter/ipt_ECN.o
  CC      net/netfilter/ipset/ip_set_hash_mac.o
  CC      drivers/scsi/scsi_lib_dma.o
  CC      net/ipv4/netfilter/ipt_REJECT.o
  CC      net/xfrm/xfrm_output.o
  CC      drivers/scsi/scsi_scan.o
  CC      net/ipv4/netfilter/ipt_SYNPROXY.o
  CC      net/netfilter/ipset/ip_set_hash_net.o
  GEN     drivers/scsi/scsi_devinfo_tbl.c
  CC      drivers/scsi/scsi_devinfo.o
  CC      net/xfrm/xfrm_sysctl.o
  CC      net/ipv4/netfilter/arp_tables.o
  CC      drivers/scsi/scsi_sysctl.o
  CC      net/xfrm/xfrm_replay.o
  CC      drivers/scsi/scsi_trace.o
  CC      drivers/scsi/scsi_logging.o
  CC      net/ipv4/netfilter/arpt_mangle.o
  CC      net/xfrm/xfrm_device.o
  CC      net/netfilter/ipset/ip_set_hash_netport.o
  CC      drivers/scsi/scsi_bsg.o
  CC      net/ipv4/netfilter/arptable_filter.o
  CC      net/xfrm/xfrm_nat_keepalive.o
  CC      drivers/scsi/scsi_common.o
  CC      net/ipv4/netfilter/nf_dup_ipv4.o
  CC      drivers/scsi/virtio_scsi.o
  CC      net/xfrm/xfrm_algo.o
  CC      net/ipv4/netfilter/nf_nat_snmp_basic.asn1.o
  CC      net/ipv4/netfilter/nf_nat_snmp_basic_main.o
  CC      drivers/scsi/sd.o
  CC      net/xfrm/xfrm_user.o
  CC      net/netfilter/ipset/ip_set_hash_netiface.o
  AR      net/ipv4/netfilter/built-in.a
  CC      net/ipv4/route.o
  CC      drivers/scsi/scsi_sysfs.o
  AR      net/xfrm/built-in.a
  CC      net/unix/af_unix.o
  CC      net/netfilter/ipset/ip_set_hash_netnet.o
  CC      net/ipv4/inetpeer.o
  AR      drivers/scsi/built-in.a
  AR      drivers/nvme/common/built-in.a
  AR      drivers/nvme/host/built-in.a
  AR      drivers/nvme/target/built-in.a
  AR      drivers/nvme/built-in.a
  AR      drivers/net/phy/qcom/built-in.a
  AR      drivers/net/phy/built-in.a
  AR      drivers/net/pse-pd/built-in.a
  AR      drivers/net/mdio/built-in.a
  AR      drivers/net/pcs/built-in.a
  CC      drivers/net/vxlan/vxlan_core.o
  CC      net/ipv4/protocol.o
  CC      net/ipv4/ip_input.o
  CC      net/unix/garbage.o
  CC      net/netfilter/ipset/ip_set_hash_netportnet.o
  CC      net/ipv4/ip_fragment.o
  CC      net/unix/sysctl_net_unix.o
  CC      drivers/net/vxlan/vxlan_multicast.o
  CC      net/unix/unix_bpf.o
  CC      net/ipv4/ip_forward.o
  CC      drivers/net/vxlan/vxlan_vnifilter.o
  AR      net/unix/built-in.a
  CC      drivers/net/vxlan/vxlan_mdb.o
  CC      net/ipv4/ip_options.o
  CC      net/netfilter/ipset/ip_set_list_set.o
  CC      net/ipv4/ip_output.o
  CC      net/netfilter/ipvs/ip_vs_conn.o
  AR      drivers/net/vxlan/built-in.a
  AR      net/netfilter/ipset/built-in.a
  AR      drivers/net/ethernet/intel/built-in.a
  AR      drivers/net/ethernet/built-in.a
  CC      drivers/net/macvlan.o
  CC      net/ipv6/netfilter/ip6_tables.o
  CC      net/ipv4/ip_sockglue.o
  CC      net/netfilter/ipvs/ip_vs_core.o
  CC      net/ipv6/netfilter/ip6table_filter.o
  CC      drivers/net/macvtap.o
  CC      drivers/net/loopback.o
  CC      net/ipv6/netfilter/ip6table_mangle.o
  CC      net/netfilter/ipvs/ip_vs_ctl.o
  CC      net/ipv4/inet_hashtables.o
  CC      drivers/net/tun.o
  CC      net/ipv6/netfilter/ip6table_raw.o
  CC      net/ipv6/netfilter/ip6table_security.o
  CC      net/ipv4/inet_timewait_sock.o
  CC      net/netfilter/ipvs/ip_vs_sched.o
  CC      net/ipv6/netfilter/ip6table_nat.o
  CC      net/ipv4/inet_connection_sock.o
  CC      net/netfilter/ipvs/ip_vs_xmit.o
  CC      net/ipv6/netfilter/nf_defrag_ipv6_hooks.o
  CC      drivers/net/tap.o
  CC      net/ipv6/netfilter/nf_conntrack_reasm.o
  CC      net/ipv4/tcp.o
  CC      net/netfilter/ipvs/ip_vs_app.o
  CC      drivers/net/veth.o
  CC      net/ipv6/netfilter/nf_socket_ipv6.o
  CC      net/netfilter/ipvs/ip_vs_sync.o
  CC      net/ipv6/netfilter/nf_tproxy_ipv6.o
  CC      drivers/net/virtio_net.o
  CC      net/netfilter/ipvs/ip_vs_est.o
  CC      net/ipv6/netfilter/nf_reject_ipv6.o
  CC      net/ipv4/tcp_input.o
  CC      net/netfilter/ipvs/ip_vs_proto.o
  CC      net/ipv6/netfilter/nf_dup_ipv6.o
  CC      net/netfilter/ipvs/ip_vs_pe.o
  CC      net/ipv6/netfilter/nft_reject_ipv6.o
  CC      drivers/net/net_failover.o
  CC      net/ipv6/netfilter/nft_dup_ipv6.o
  CC      net/netfilter/ipvs/ip_vs_proto_tcp.o
  CC      net/ipv6/netfilter/nft_fib_ipv6.o
  AR      drivers/net/built-in.a
  AR      drivers/firewire/built-in.a
  CC      drivers/vfio/pci/vfio_pci_core.o
  CC      net/netfilter/ipvs/ip_vs_proto_udp.o
  CC      net/ipv6/netfilter/ip6t_ah.o
  CC      net/ipv4/tcp_output.o
  CC      drivers/vfio/pci/vfio_pci_intrs.o
  CC      net/netfilter/ipvs/ip_vs_proto_ah_esp.o
  CC      net/ipv6/netfilter/ip6t_eui64.o
  CC      drivers/vfio/pci/vfio_pci_rdwr.o
  CC      net/netfilter/ipvs/ip_vs_proto_sctp.o
  CC      net/ipv6/netfilter/ip6t_frag.o
  CC      drivers/vfio/pci/vfio_pci_config.o
  CC      net/netfilter/ipvs/ip_vs_nfct.o
  CC      net/ipv6/netfilter/ip6t_ipv6header.o
  CC      drivers/vfio/pci/vfio_pci.o
  CC      net/ipv4/tcp_timer.o
  CC      net/netfilter/ipvs/ip_vs_rr.o
  AR      drivers/vfio/pci/built-in.a
  CC      drivers/vfio/vfio_main.o
  CC      net/ipv6/netfilter/ip6t_mh.o
  CC      net/netfilter/ipvs/ip_vs_wrr.o
  CC      net/ipv4/tcp_ipv4.o
  CC      drivers/vfio/group.o
  CC      net/ipv6/netfilter/ip6t_hbh.o
  CC      net/netfilter/ipvs/ip_vs_lc.o
  CC      drivers/vfio/container.o
  CC      net/ipv6/netfilter/ip6t_rpfilter.o
  CC      net/netfilter/ipvs/ip_vs_wlc.o
  CC      drivers/vfio/virqfd.o
  CC      net/ipv6/netfilter/ip6t_rt.o
  CC      drivers/vfio/vfio_iommu_type1.o
  CC      net/netfilter/ipvs/ip_vs_fo.o
  CC      net/ipv4/tcp_minisocks.o
  CC      net/ipv6/netfilter/ip6t_srh.o
  CC      net/netfilter/ipvs/ip_vs_ovf.o
  CC      net/ipv4/tcp_cong.o
  CC      net/ipv6/netfilter/ip6t_NPT.o
  AR      drivers/vfio/built-in.a
  AR      drivers/cdrom/built-in.a
  AR      drivers/auxdisplay/built-in.a
  AR      drivers/usb/built-in.a
  CC      drivers/input/input.o
  CC      net/netfilter/ipvs/ip_vs_lblc.o
  CC      net/ipv4/tcp_metrics.o
  CC      net/ipv6/netfilter/ip6t_REJECT.o
  CC      net/netfilter/ipvs/ip_vs_lblcr.o
  CC      drivers/input/input-compat.o
  CC      drivers/input/input-mt.o
  CC      net/ipv6/netfilter/ip6t_SYNPROXY.o
  CC      net/ipv4/tcp_fastopen.o
  CC      drivers/input/input-poller.o
  CC      net/netfilter/ipvs/ip_vs_dh.o
  CC      drivers/input/ff-core.o
  AR      net/ipv6/netfilter/built-in.a
  CC      net/ipv6/af_inet6.o
  CC      drivers/input/touchscreen.o
  CC      net/ipv4/tcp_rate.o
  CC      net/netfilter/ipvs/ip_vs_sh.o
  AR      drivers/input/built-in.a
  CC      drivers/rtc/lib.o
  CC      drivers/rtc/class.o
  CC      net/ipv6/anycast.o
  CC      net/ipv4/tcp_recovery.o
  CC      net/netfilter/ipvs/ip_vs_sed.o
  CC      drivers/rtc/interface.o
  CC      net/ipv4/tcp_ulp.o
  CC      net/netfilter/ipvs/ip_vs_nq.o
  CC      drivers/rtc/dev.o
  CC      net/ipv6/ip6_output.o
  CC      drivers/rtc/proc.o
  CC      net/ipv4/tcp_offload.o
  CC      net/netfilter/ipvs/ip_vs_ftp.o
  CC      drivers/rtc/sysfs.o
  CC      drivers/rtc/rtc-efi.o
  CC      net/netfilter/ipvs/ip_vs_pe_sip.o
  CC      net/ipv4/tcp_plb.o
  CC      drivers/rtc/rtc-pl031.o
  CC      net/ipv6/ip6_input.o
  AR      drivers/rtc/built-in.a
  AR      net/netfilter/ipvs/built-in.a
  CC      net/netfilter/core.o
  AR      drivers/i2c/algos/built-in.a
  AR      drivers/i2c/busses/built-in.a
  CC      net/ipv4/datagram.o
  AR      drivers/i2c/muxes/built-in.a
  AR      drivers/i2c/built-in.a
  AR      drivers/i3c/built-in.a
  AR      drivers/media/i2c/built-in.a
  AR      drivers/media/tuners/built-in.a
  AR      drivers/media/rc/keymaps/built-in.a
  AR      drivers/media/rc/built-in.a
  AR      drivers/media/common/b2c2/built-in.a
  AR      drivers/media/common/saa7146/built-in.a
  AR      drivers/media/common/siano/built-in.a
  AR      drivers/media/common/v4l2-tpg/built-in.a
  AR      drivers/media/common/videobuf2/built-in.a
  AR      drivers/media/common/built-in.a
  AR      drivers/media/platform/allegro-dvt/built-in.a
  AR      drivers/media/platform/amlogic/meson-ge2d/built-in.a
  AR      drivers/media/platform/amlogic/built-in.a
  AR      drivers/media/platform/amphion/built-in.a
  AR      drivers/media/platform/aspeed/built-in.a
  AR      drivers/media/platform/atmel/built-in.a
  AR      drivers/media/platform/broadcom/built-in.a
  AR      drivers/media/platform/cadence/built-in.a
  AR      drivers/media/platform/chips-media/coda/built-in.a
  AR      drivers/media/platform/chips-media/wave5/built-in.a
  AR      drivers/media/platform/chips-media/built-in.a
  AR      drivers/media/platform/imagination/built-in.a
  AR      drivers/media/platform/intel/built-in.a
  AR      drivers/media/platform/marvell/built-in.a
  AR      drivers/media/platform/mediatek/jpeg/built-in.a
  AR      drivers/media/platform/mediatek/mdp/built-in.a
  AR      drivers/media/platform/mediatek/vcodec/common/built-in.a
  AR      drivers/media/platform/mediatek/vcodec/encoder/built-in.a
  AR      drivers/media/platform/mediatek/vcodec/decoder/built-in.a
  AR      drivers/media/platform/mediatek/vcodec/built-in.a
  AR      drivers/media/platform/mediatek/vpu/built-in.a
  AR      drivers/media/platform/mediatek/mdp3/built-in.a
  AR      drivers/media/platform/mediatek/built-in.a
  AR      drivers/media/platform/microchip/built-in.a
  AR      drivers/media/platform/nuvoton/built-in.a
  AR      drivers/media/platform/nvidia/tegra-vde/built-in.a
  AR      drivers/media/platform/nvidia/built-in.a
  AR      drivers/media/platform/nxp/dw100/built-in.a
  AR      drivers/media/platform/nxp/imx-jpeg/built-in.a
  AR      drivers/media/platform/nxp/imx8-isi/built-in.a
  AR      drivers/media/platform/nxp/built-in.a
  AR      drivers/media/platform/qcom/camss/built-in.a
  AR      drivers/media/platform/qcom/venus/built-in.a
  AR      drivers/media/platform/qcom/built-in.a
  AR      drivers/media/platform/raspberrypi/pisp_be/built-in.a
  AR      drivers/media/platform/raspberrypi/built-in.a
  AR      drivers/media/platform/renesas/rcar-vin/built-in.a
  AR      drivers/media/platform/renesas/rzg2l-cru/built-in.a
  AR      drivers/media/platform/renesas/vsp1/built-in.a
  AR      drivers/media/platform/renesas/built-in.a
  AR      drivers/media/platform/rockchip/rga/built-in.a
  AR      drivers/media/platform/rockchip/rkisp1/built-in.a
  AR      drivers/media/platform/rockchip/built-in.a
  AR      drivers/media/platform/samsung/exynos-gsc/built-in.a
  CC      net/ipv6/addrconf.o
  AR      drivers/media/platform/samsung/exynos4-is/built-in.a
  AR      drivers/media/platform/samsung/s3c-camif/built-in.a
  AR      drivers/media/platform/samsung/s5p-g2d/built-in.a
  AR      drivers/media/platform/samsung/s5p-jpeg/built-in.a
  AR      drivers/media/platform/samsung/s5p-mfc/built-in.a
  AR      drivers/media/platform/samsung/built-in.a
  AR      drivers/media/platform/st/sti/bdisp/built-in.a
  AR      drivers/media/platform/st/sti/c8sectpfe/built-in.a
  AR      drivers/media/platform/st/sti/delta/built-in.a
  AR      drivers/media/platform/st/sti/hva/built-in.a
  AR      drivers/media/platform/st/stm32/built-in.a
  AR      drivers/media/platform/st/built-in.a
  AR      drivers/media/platform/sunxi/sun4i-csi/built-in.a
  AR      drivers/media/platform/sunxi/sun6i-csi/built-in.a
  AR      drivers/media/platform/sunxi/sun6i-mipi-csi2/built-in.a
  AR      drivers/media/platform/sunxi/sun8i-a83t-mipi-csi2/built-in.a
  AR      drivers/media/platform/sunxi/sun8i-di/built-in.a
  AR      drivers/media/platform/sunxi/sun8i-rotate/built-in.a
  AR      drivers/media/platform/sunxi/built-in.a
  AR      drivers/media/platform/ti/am437x/built-in.a
  AR      drivers/media/platform/ti/cal/built-in.a
  AR      drivers/media/platform/ti/vpe/built-in.a
  AR      drivers/media/platform/ti/davinci/built-in.a
  CC      net/ipv4/raw.o
  AR      drivers/media/platform/ti/j721e-csi2rx/built-in.a
  AR      drivers/media/platform/ti/omap/built-in.a
  AR      drivers/media/platform/ti/omap3isp/built-in.a
  AR      drivers/media/platform/ti/built-in.a
  AR      drivers/media/platform/verisilicon/built-in.a
  AR      drivers/media/platform/via/built-in.a
  AR      drivers/media/platform/xilinx/built-in.a
  AR      drivers/media/platform/built-in.a
  AR      drivers/media/pci/ttpci/built-in.a
  AR      drivers/media/pci/b2c2/built-in.a
  AR      drivers/media/pci/pluto2/built-in.a
  AR      drivers/media/pci/dm1105/built-in.a
  CC      net/netfilter/nf_log.o
  AR      drivers/media/pci/pt1/built-in.a
  AR      drivers/media/pci/pt3/built-in.a
  AR      drivers/media/pci/mantis/built-in.a
  AR      drivers/media/pci/ngene/built-in.a
  AR      drivers/media/pci/ddbridge/built-in.a
  AR      drivers/media/pci/saa7146/built-in.a
  AR      drivers/media/pci/smipcie/built-in.a
  AR      drivers/media/pci/netup_unidvb/built-in.a
  AR      drivers/media/pci/intel/ipu3/built-in.a
  AR      drivers/media/pci/intel/ivsc/built-in.a
  AR      drivers/media/pci/intel/built-in.a
  AR      drivers/media/pci/built-in.a
  AR      drivers/media/usb/b2c2/built-in.a
  AR      drivers/media/usb/dvb-usb/built-in.a
  AR      drivers/media/usb/dvb-usb-v2/built-in.a
  AR      drivers/media/usb/s2255/built-in.a
  AR      drivers/media/usb/siano/built-in.a
  AR      drivers/media/usb/ttusb-budget/built-in.a
  AR      drivers/media/usb/ttusb-dec/built-in.a
  AR      drivers/media/usb/built-in.a
  AR      drivers/media/mmc/siano/built-in.a
  AR      drivers/media/mmc/built-in.a
  AR      drivers/media/firewire/built-in.a
  AR      drivers/media/spi/built-in.a
  AR      drivers/media/test-drivers/built-in.a
  AR      drivers/media/built-in.a
  AR      drivers/pps/clients/built-in.a
  AR      drivers/pps/generators/built-in.a
  CC      drivers/pps/pps.o
  CC      drivers/pps/kapi.o
  CC      net/netfilter/nf_queue.o
  CC      drivers/pps/sysfs.o
  CC      net/ipv4/udp.o
  AR      drivers/pps/built-in.a
  CC      drivers/ptp/ptp_clock.o
  CC      net/netfilter/nf_sockopt.o
  CC      drivers/ptp/ptp_chardev.o
  CC      net/netfilter/utils.o
  CC      drivers/ptp/ptp_sysfs.o
  CC      net/ipv6/addrlabel.o
  CC      net/netfilter/nf_bpf_link.o
  CC      drivers/ptp/ptp_vclock.o
  CC      net/ipv4/udplite.o
  CC      net/ipv6/route.o
  CC      net/netfilter/nfnetlink.o
  CC      drivers/ptp/ptp_kvm_arm.o
  CC      drivers/ptp/ptp_kvm_common.o
  CC      net/ipv4/udp_offload.o
  AR      drivers/ptp/built-in.a
  AR      drivers/power/reset/built-in.a
  CC      drivers/power/supply/power_supply_core.o
  CC      net/netfilter/nfnetlink_acct.o
  CC      net/ipv4/arp.o
  CC      drivers/power/supply/power_supply_sysfs.o
  CC      net/netfilter/nfnetlink_queue.o
  AR      drivers/power/supply/built-in.a
  AR      drivers/power/built-in.a
  AR      drivers/thermal/broadcom/built-in.a
  AR      drivers/thermal/renesas/built-in.a
  AR      drivers/thermal/samsung/built-in.a
  AR      drivers/thermal/intel/built-in.a
  AR      drivers/thermal/st/built-in.a
  AR      drivers/thermal/qcom/built-in.a
  AR      drivers/thermal/tegra/built-in.a
  AR      drivers/thermal/mediatek/built-in.a
  CC      drivers/thermal/thermal_core.o
  CC      net/ipv4/icmp.o
  CC      net/ipv6/ip6_fib.o
  CC      drivers/thermal/thermal_sysfs.o
  CC      net/netfilter/nfnetlink_log.o
  CC      drivers/thermal/thermal_trip.o
  CC      drivers/thermal/thermal_helpers.o
  CC      net/ipv4/devinet.o
  CC      drivers/thermal/gov_step_wise.o
  CC      net/netfilter/nfnetlink_osf.o
  AR      drivers/thermal/built-in.a
  CC      drivers/cpufreq/cpufreq.o
  CC      net/ipv6/ipv6_sockglue.o
  CC      net/netfilter/nf_conntrack_core.o
  CC      net/ipv4/af_inet.o
  CC      net/ipv6/ndisc.o
  CC      drivers/cpufreq/freq_table.o
  CC      drivers/cpufreq/cpufreq_performance.o
  AR      drivers/cpufreq/built-in.a
  CC      drivers/cpuidle/governors/menu.o
  CC      net/ipv4/igmp.o
  AR      drivers/cpuidle/governors/built-in.a
  CC      drivers/cpuidle/cpuidle.o
  CC      net/netfilter/nf_conntrack_standalone.o
  CC      net/ipv6/udp.o
  CC      drivers/cpuidle/driver.o
  CC      net/netfilter/nf_conntrack_expect.o
  CC      drivers/cpuidle/governor.o
  CC      drivers/cpuidle/sysfs.o
  CC      net/ipv4/fib_frontend.o
  AR      drivers/cpuidle/built-in.a
  AR      drivers/mmc/built-in.a
  AR      drivers/ufs/built-in.a
  AR      drivers/firmware/arm_ffa/built-in.a
  AR      drivers/firmware/arm_scmi/built-in.a
  AR      drivers/firmware/broadcom/built-in.a
  AR      drivers/firmware/cirrus/built-in.a
  AR      drivers/firmware/meson/built-in.a
  AR      drivers/firmware/microchip/built-in.a
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
  CC      drivers/firmware/efi/libstub/printk.o
  CC      net/ipv6/reassembly.o
  CC      net/netfilter/nf_conntrack_extend.o
  CC      drivers/firmware/efi/libstub/vsprintf.o
  CC      net/ipv4/ping.o
  CC      drivers/firmware/efi/libstub/fdt.o
  CC      net/ipv6/tcp_ipv6.o
  CC      net/netfilter/nf_conntrack_acct.o
  CC      drivers/firmware/efi/libstub/lib-fdt_rw.o
  CC      drivers/firmware/efi/libstub/lib-fdt_ro.o
  CC      net/ipv4/ip_tunnel_core.o
  CC      drivers/firmware/efi/libstub/lib-fdt_wip.o
  CC      drivers/firmware/efi/libstub/lib-fdt.o
  CC      net/netfilter/nf_conntrack_seqadj.o
  CC      drivers/firmware/efi/libstub/lib-fdt_empty_tree.o
  CC      drivers/firmware/efi/libstub/lib-fdt_sw.o
  CC      drivers/firmware/efi/libstub/efi-stub.o
  CC      net/ipv4/gre_offload.o
  CC      drivers/firmware/efi/libstub/string.o
  CC      drivers/firmware/efi/libstub/intrinsics.o
  CC      net/netfilter/nf_conntrack_proto_icmpv6.o
  CC      net/ipv6/ping.o
  CC      drivers/firmware/efi/libstub/systable.o
  CC      net/ipv4/metrics.o
  CC      drivers/firmware/efi/libstub/screen_info.o
  CC      net/netfilter/nf_conntrack_timeout.o
  CC      net/ipv6/exthdrs.o
  CC      drivers/firmware/efi/libstub/efi-stub-entry.o
  CC      net/ipv4/netlink.o
  CC      drivers/firmware/efi/libstub/kaslr.o
  CC      net/netfilter/nf_conntrack_timestamp.o
  CC      drivers/firmware/efi/libstub/arm64.o
  CC      net/ipv4/nexthop.o
  CC      net/ipv6/datagram.o
  CC      drivers/firmware/efi/libstub/arm64-stub.o
  CC      net/netfilter/nf_conntrack_ecache.o
  CC      drivers/firmware/efi/libstub/smbios.o
  STUBCPY drivers/firmware/efi/libstub/alignedmem.stub.o
  STUBCPY drivers/firmware/efi/libstub/arm64-stub.stub.o
  STUBCPY drivers/firmware/efi/libstub/arm64.stub.o
  STUBCPY drivers/firmware/efi/libstub/efi-stub-entry.stub.o
  CC      net/ipv6/ip6_flowlabel.o
  STUBCPY drivers/firmware/efi/libstub/efi-stub-helper.stub.o
  STUBCPY drivers/firmware/efi/libstub/efi-stub.stub.o
  STUBCPY drivers/firmware/efi/libstub/fdt.stub.o
  STUBCPY drivers/firmware/efi/libstub/file.stub.o
  STUBCPY drivers/firmware/efi/libstub/gop.stub.o
  STUBCPY drivers/firmware/efi/libstub/intrinsics.stub.o
  STUBCPY drivers/firmware/efi/libstub/kaslr.stub.o
  STUBCPY drivers/firmware/efi/libstub/lib-cmdline.stub.o
  STUBCPY drivers/firmware/efi/libstub/lib-ctype.stub.o
  STUBCPY drivers/firmware/efi/libstub/lib-fdt.stub.o
  STUBCPY drivers/firmware/efi/libstub/lib-fdt_empty_tree.stub.o
  STUBCPY drivers/firmware/efi/libstub/lib-fdt_ro.stub.o
  STUBCPY drivers/firmware/efi/libstub/lib-fdt_rw.stub.o
  STUBCPY drivers/firmware/efi/libstub/lib-fdt_sw.stub.o
  CC      net/netfilter/nf_conntrack_labels.o
  STUBCPY drivers/firmware/efi/libstub/lib-fdt_wip.stub.o
  STUBCPY drivers/firmware/efi/libstub/mem.stub.o
  STUBCPY drivers/firmware/efi/libstub/pci.stub.o
  STUBCPY drivers/firmware/efi/libstub/printk.stub.o
  STUBCPY drivers/firmware/efi/libstub/random.stub.o
  STUBCPY drivers/firmware/efi/libstub/randomalloc.stub.o
  STUBCPY drivers/firmware/efi/libstub/relocate.stub.o
  STUBCPY drivers/firmware/efi/libstub/screen_info.stub.o
  STUBCPY drivers/firmware/efi/libstub/secureboot.stub.o
  STUBCPY drivers/firmware/efi/libstub/skip_spaces.stub.o
  STUBCPY drivers/firmware/efi/libstub/smbios.stub.o
  STUBCPY drivers/firmware/efi/libstub/string.stub.o
  STUBCPY drivers/firmware/efi/libstub/systable.stub.o
  STUBCPY drivers/firmware/efi/libstub/tpm.stub.o
  STUBCPY drivers/firmware/efi/libstub/vsprintf.stub.o
  AR      drivers/firmware/efi/libstub/lib.a
  CC      drivers/firmware/efi/efi.o
  CC      net/ipv4/udp_tunnel_stub.o
  CC      net/netfilter/nf_conntrack_proto_dccp.o
  CC      net/ipv6/inet6_connection_sock.o
  CC      drivers/firmware/efi/vars.o
  CC      drivers/firmware/efi/reboot.o
  CC      net/ipv4/ip_tunnel.o
  CC      net/netfilter/nf_conntrack_proto_sctp.o
  CC      drivers/firmware/efi/memattr.o
  CC      net/ipv6/udp_offload.o
  CC      drivers/firmware/efi/tpm.o
  CC      net/netfilter/nf_conntrack_proto_gre.o
  CC      net/ipv6/seg6.o
  CC      drivers/firmware/efi/memmap.o
  CC      net/ipv4/sysctl_net_ipv4.o
  CC      drivers/firmware/efi/fdtparams.o
  CC      net/ipv6/fib6_notifier.o
  CC      net/netfilter/nf_conntrack_netlink.o
  CC      drivers/firmware/efi/esrt.o
  CC      net/ipv4/proc.o
  CC      drivers/firmware/efi/runtime-wrappers.o
  CC      net/ipv6/rpl.o
  CC      drivers/firmware/efi/efi-init.o
  CC      net/ipv6/ioam6.o
  CC      net/ipv4/fib_rules.o
  CC      drivers/firmware/efi/arm-runtime.o
  CC      net/netfilter/nfnetlink_cttimeout.o
  CC      drivers/firmware/efi/earlycon.o
  CC      net/ipv4/udp_tunnel_core.o
  CC      net/ipv6/sysctl_net_ipv6.o
  AR      drivers/firmware/efi/built-in.a
  AR      drivers/firmware/imx/built-in.a
  CC      drivers/firmware/psci/psci.o
  CC      net/netfilter/nfnetlink_cthelper.o
  CC      net/ipv6/xfrm6_policy.o
  AR      drivers/firmware/psci/built-in.a
  AR      drivers/firmware/qcom/built-in.a
  CC      drivers/firmware/smccc/smccc.o
  CC      net/ipv4/udp_tunnel_nic.o
  CC      drivers/firmware/smccc/kvm_guest.o
  AR      drivers/firmware/smccc/built-in.a
  AR      drivers/firmware/tegra/built-in.a
  AR      drivers/firmware/xilinx/built-in.a
  AR      drivers/firmware/built-in.a
  AR      drivers/crypto/stm32/built-in.a
  AR      drivers/crypto/xilinx/built-in.a
  AR      drivers/crypto/hisilicon/built-in.a
  AR      drivers/crypto/intel/keembay/built-in.a
  AR      drivers/crypto/intel/ixp4xx/built-in.a
  AR      drivers/crypto/intel/built-in.a
  AR      drivers/crypto/starfive/built-in.a
  AR      drivers/crypto/built-in.a
  CC      drivers/clocksource/timer-of.o
  CC      net/netfilter/nf_conntrack_amanda.o
  CC      net/ipv6/xfrm6_state.o
  CC      drivers/clocksource/timer-probe.o
  CC      net/ipv4/syncookies.o
  CC      drivers/clocksource/arm_arch_timer.o
  CC      net/ipv6/xfrm6_input.o
  CC      net/netfilter/nf_conntrack_ftp.o
  CC      net/ipv4/esp4.o
  CC      drivers/clocksource/dummy_timer.o
  CC      net/ipv6/xfrm6_output.o
  AR      drivers/clocksource/built-in.a
  CC      drivers/of/base.o
  CC      net/netfilter/nf_conntrack_h323_main.o
  CC      net/ipv6/xfrm6_protocol.o
  CC      net/ipv4/ipconfig.o
  CC      drivers/of/cpu.o
  CC      net/netfilter/nf_conntrack_h323_asn1.o
  CC      drivers/of/device.o
  CC      net/ipv6/netfilter.o
  CC      net/netfilter/nf_conntrack_irc.o
  CC      drivers/of/module.o
  CC      net/ipv4/netfilter.o
  CC      drivers/of/platform.o
  CC      net/ipv6/fib6_rules.o
  CC      net/netfilter/nf_conntrack_broadcast.o
  CC      net/ipv4/tcp_bbr.o
  CC      drivers/of/property.o
  CC      net/ipv6/proc.o
  CC      net/netfilter/nf_conntrack_netbios_ns.o
  CC      net/ipv4/tcp_cubic.o
  CC      drivers/of/kobj.o
  CC      net/netfilter/nf_conntrack_snmp.o
  CC      drivers/of/fdt.o
  CC      net/ipv6/syncookies.o
  CC      net/ipv4/tcp_sigpool.o
  CC      net/netfilter/nf_conntrack_pptp.o
  DTC     drivers/of/empty_root.dtb
  CC      drivers/of/fdt_address.o
  CC      net/ipv6/addrconf_core.o
  CC      drivers/of/address.o
  CC      net/ipv4/tcp_bpf.o
  CC      net/netfilter/nf_conntrack_sane.o
  CC      net/ipv6/exthdrs_core.o
  CC      drivers/of/irq.o
  CC      net/netfilter/nf_conntrack_sip.o
  CC      drivers/of/of_reserved_mem.o
  CC      net/ipv6/ip6_checksum.o
  CC      net/ipv4/udp_bpf.o
  CC      drivers/of/of_numa.o
  CC      net/ipv6/ip6_icmp.o
  WRAP    drivers/of/empty_root.dtb.S
  AS      drivers/of/empty_root.dtb.o
  AR      drivers/of/built-in.a
  AR      drivers/platform/built-in.a
  AR      drivers/perf/built-in.a
  AR      drivers/hwtracing/intel_th/built-in.a
  AR      drivers/android/built-in.a
  AR      drivers/nvmem/layouts/built-in.a
  CC      drivers/nvmem/core.o
  CC      net/ipv4/xfrm4_policy.o
  CC      net/netfilter/nf_conntrack_tftp.o
  CC      net/ipv6/output_core.o
  CC      drivers/nvmem/layouts.o
  CC      net/ipv4/xfrm4_state.o
  CC      net/netfilter/nf_log_syslog.o
  AR      drivers/nvmem/built-in.a
  AR      drivers/built-in.a
  CC      net/netfilter/nf_nat_core.o
  CC      net/ipv6/protocol.o
  CC      net/ipv4/xfrm4_input.o
  CC      net/ipv6/ip6_offload.o
  CC      net/netfilter/nf_nat_proto.o
  CC      net/ipv6/tcpv6_offload.o
  CC      net/ipv4/xfrm4_output.o
  CC      net/ipv6/exthdrs_offload.o
  CC      net/ipv4/xfrm4_protocol.o
  CC      net/netfilter/nf_nat_helper.o
  CC      net/ipv6/inet6_hashtables.o
  CC      net/netfilter/nf_nat_redirect.o
  AR      net/ipv4/built-in.a
  CC      net/packet/af_packet.o
  CC      net/netfilter/nf_nat_masquerade.o
  CC      net/ipv6/ip6_udp_tunnel.o
  CC      net/bridge/netfilter/nft_meta_bridge.o
  CC      net/netfilter/nf_nat_amanda.o
  CC      net/ipv6/mcast_snoop.o
  CC      net/bridge/netfilter/nft_reject_bridge.o
  CC      net/netfilter/nf_nat_ftp.o
  AR      net/ipv6/built-in.a
  CC      net/packet/diag.o
  AR      net/bridge/netfilter/built-in.a
  CC      net/bridge/br.o
  CC      net/netfilter/nf_nat_irc.o
  AR      net/dsa/built-in.a
  CC      net/9p/mod.o
  AR      net/packet/built-in.a
  CC      net/vmw_vsock/af_vsock.o
  CC      net/9p/client.o
  CC      net/bridge/br_device.o
  CC      net/netfilter/nf_nat_sip.o
  CC      net/bridge/br_fdb.o
  CC      net/9p/error.o
  CC      net/vmw_vsock/af_vsock_tap.o
  CC      net/netfilter/nf_nat_tftp.o
  CC      net/9p/protocol.o
  CC      net/vmw_vsock/vsock_addr.o
  CC      net/netfilter/nf_synproxy_core.o
  CC      net/9p/trans_common.o
  CC      net/9p/trans_virtio.o
  CC      net/bridge/br_forward.o
  CC      net/vmw_vsock/vsock_bpf.o
  CC      net/netfilter/nf_conncount.o
  CC      net/bridge/br_if.o
  AR      net/9p/built-in.a
  CC      net/switchdev/switchdev.o
  CC      net/vmw_vsock/virtio_transport.o
  CC      net/netfilter/nf_dup_netdev.o
  AR      net/switchdev/built-in.a
  CC      net/devres.o
  CC      net/vmw_vsock/virtio_transport_common.o
  CC      net/bridge/br_input.o
  CC      net/socket.o
  CC      net/netfilter/nf_tables_core.o
  CC      net/bridge/br_ioctl.o
  AR      net/vmw_vsock/built-in.a
  CC      net/sysctl_net.o
  CC      net/netfilter/nf_tables_api.o
  CC      net/bridge/br_stp.o
  CC      net/bridge/br_stp_bpdu.o
  CC      net/netfilter/nft_chain_filter.o
  CC      net/bridge/br_stp_if.o
  CC      net/bridge/br_stp_timer.o
  CC      net/bridge/br_netlink.o
  CC      net/netfilter/nf_tables_trace.o
  CC      net/bridge/br_netlink_tunnel.o
  CC      net/netfilter/nft_immediate.o
  CC      net/bridge/br_arp_nd_proxy.o
  CC      net/bridge/br_sysfs_if.o
  CC      net/netfilter/nft_cmp.o
  CC      net/bridge/br_sysfs_br.o
  CC      net/bridge/br_nf_core.o
  CC      net/netfilter/nft_range.o
  CC      net/bridge/br_multicast.o
  CC      net/netfilter/nft_bitwise.o
  CC      net/netfilter/nft_byteorder.o
  CC      net/netfilter/nft_payload.o
  CC      net/bridge/br_mdb.o
  CC      net/netfilter/nft_lookup.o
  CC      net/bridge/br_multicast_eht.o
  CC      net/netfilter/nft_dynset.o
  CC      net/bridge/br_switchdev.o
  CC      net/netfilter/nft_meta.o
  CC      net/bridge/br_netfilter_hooks.o
  CC      net/bridge/br_netfilter_ipv6.o
  CC      net/netfilter/nft_rt.o
  CC      net/netfilter/nft_exthdr.o
  CC      net/netfilter/nft_last.o
  CC      net/netfilter/nft_counter.o
  AR      net/bridge/built-in.a
  CC      net/netfilter/nft_objref.o
  CC      net/netfilter/nft_inner.o
  CC      net/netfilter/nft_chain_route.o
  CC      net/netfilter/nf_tables_offload.o
  CC      net/netfilter/nft_set_hash.o
  CC      net/netfilter/nft_set_bitmap.o
  CC      net/netfilter/nft_set_rbtree.o
  CC      net/netfilter/nft_set_pipapo.o
  CC      net/netfilter/nft_compat.o
  CC      net/netfilter/nft_connlimit.o
  CC      net/netfilter/nft_numgen.o
  CC      net/netfilter/nft_ct.o
  CC      net/netfilter/nft_limit.o
  CC      net/netfilter/nft_nat.o
  CC      net/netfilter/nft_queue.o
  CC      net/netfilter/nft_quota.o
  CC      net/netfilter/nft_reject.o
  CC      net/netfilter/nft_reject_inet.o
  CC      net/netfilter/nft_tunnel.o
  CC      net/netfilter/nft_log.o
  CC      net/netfilter/nft_masq.o
  CC      net/netfilter/nft_redir.o
  CC      net/netfilter/nft_hash.o
  CC      net/netfilter/nft_fib.o
  CC      net/netfilter/nft_fib_inet.o
  CC      net/netfilter/nft_fib_netdev.o
  CC      net/netfilter/nft_socket.o
  CC      net/netfilter/nft_osf.o
  CC      net/netfilter/nft_tproxy.o
  CC      net/netfilter/nft_xfrm.o
  CC      net/netfilter/nft_synproxy.o
  CC      net/netfilter/nft_chain_nat.o
  CC      net/netfilter/nft_dup_netdev.o
  CC      net/netfilter/nft_fwd_netdev.o
  CC      net/netfilter/x_tables.o
  CC      net/netfilter/xt_tcpudp.o
  CC      net/netfilter/xt_mark.o
  CC      net/netfilter/xt_connmark.o
  CC      net/netfilter/xt_set.o
  CC      net/netfilter/xt_nat.o
  CC      net/netfilter/xt_CHECKSUM.o
  CC      net/netfilter/xt_CLASSIFY.o
  CC      net/netfilter/xt_CT.o
  CC      net/netfilter/xt_DSCP.o
  CC      net/netfilter/xt_HL.o
  CC      net/netfilter/xt_HMARK.o
  CC      net/netfilter/xt_LOG.o
  CC      net/netfilter/xt_NETMAP.o
  CC      net/netfilter/xt_NFLOG.o
  CC      net/netfilter/xt_NFQUEUE.o
  CC      net/netfilter/xt_RATEEST.o
  CC      net/netfilter/xt_REDIRECT.o
  CC      net/netfilter/xt_MASQUERADE.o
  CC      net/netfilter/xt_TPROXY.o
  CC      net/netfilter/xt_TCPMSS.o
  CC      net/netfilter/xt_TCPOPTSTRIP.o
  CC      net/netfilter/xt_TEE.o
  CC      net/netfilter/xt_TRACE.o
  CC      net/netfilter/xt_IDLETIMER.o
  CC      net/netfilter/xt_addrtype.o
  CC      net/netfilter/xt_bpf.o
  CC      net/netfilter/xt_cluster.o
  CC      net/netfilter/xt_comment.o
  CC      net/netfilter/xt_connbytes.o
  CC      net/netfilter/xt_connlabel.o
  CC      net/netfilter/xt_connlimit.o
  CC      net/netfilter/xt_conntrack.o
  CC      net/netfilter/xt_cpu.o
  CC      net/netfilter/xt_dccp.o
  CC      net/netfilter/xt_devgroup.o
  CC      net/netfilter/xt_dscp.o
  CC      net/netfilter/xt_ecn.o
  CC      net/netfilter/xt_esp.o
  CC      net/netfilter/xt_hashlimit.o
  CC      net/netfilter/xt_helper.o
  CC      net/netfilter/xt_hl.o
  CC      net/netfilter/xt_ipcomp.o
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
 Line 514: '[' '' == confidential ']'
 Line 517: '[' arm64 '!=' powerpc ']'
 Line 517: '[' -e arch/arm64/boot/bzImage ']'
 Line 517: '[' -e arch/arm64/boot/Image.gz ']'
 Line 518: '[' -e vmlinux ']'
 Line 519: '[' '' == firecracker ']'
 Line 519: '[' '' == cloud-hypervisor ']'
 Line 520: popd
 Line 522: [[ '' == \n\v\i\d\i\a ]]
 Line 623: getopts a:b:c:dD:eEfg:hH:k:mp:r:st:u:v:x opt
 Line 695: shift 5
 Line 697: subcmd=install
 Line 699: '[' -z install ']'
 Line 701: [[ '' == \e\x\p\e\r\i\m\e\n\t\a\l ]]
 Line 712: '[' -z 6.12.47 ']'
 Line 737: kernel_version=6.12.47
 Line 739: '[' -z '' ']'
  Line 740: get_config_version
  Line 421: get_config_and_patches
  Line 415: '[' -z '' ']'
  Line 416: patches_path=/root/kata-containers/tools/packaging/kernel/patches
  Line 422: config_version_file=/root/kata-containers/tools/packaging/kernel/patches/../kata_config_version
  Line 423: '[' -f /root/kata-containers/tools/packaging/kernel/patches/../kata_config_version ']'
  Line 424: cat /root/kata-containers/tools/packaging/kernel/patches/../kata_config_version
 Line 740: config_version=182
 Line 741: [[ '' != '' ]]
 Line 744: kernel_path=/root/kata-containers/tools/packaging/kernel/kata-linux-6.12.47-182
 Line 746: info 'Config version: 182'
 Line 52: echo 'INFO: Config version: 182'
INFO: Config version: 182
 Line 749: info 'Kernel version: 6.12.47'
 Line 52: echo 'INFO: Kernel version: 6.12.47'
INFO: Kernel version: 6.12.47
  Line 751: uname -m
 Line 751: '[' aarch64 '!=' '' -a aarch64 '!=' aarch64 ']'
 Line 753: case "${subcmd}" in
 Line 761: install_kata /root/kata-containers/tools/packaging/kernel/kata-linux-6.12.47-182
 Line 562: local kernel_path=/root/kata-containers/tools/packaging/kernel/kata-linux-6.12.47-182
 Line 563: '[' -n /root/kata-containers/tools/packaging/kernel/kata-linux-6.12.47-182 ']'
 Line 564: '[' -d /root/kata-containers/tools/packaging/kernel/kata-linux-6.12.47-182 ']'
 Line 565: '[' -n aarch64 ']'
  Line 566: arch_to_kernel aarch64
  Line 125: local -r arch=aarch64
  Line 127: case "$arch" in
  Line 128: echo arm64
 Line 566: arch_target=arm64
 Line 567: pushd /root/kata-containers/tools/packaging/kernel/kata-linux-6.12.47-182
  Line 568: get_config_version
  Line 421: get_config_and_patches
  Line 415: '[' -z '' ']'
  Line 416: patches_path=/root/kata-containers/tools/packaging/kernel/patches
  Line 422: config_version_file=/root/kata-containers/tools/packaging/kernel/patches/../kata_config_version
  Line 423: '[' -f /root/kata-containers/tools/packaging/kernel/patches/../kata_config_version ']'
  Line 424: cat /root/kata-containers/tools/packaging/kernel/patches/../kata_config_version
 Line 568: config_version=182
 Line 569: '[' -n 182 ']'
  Line 570: readlink -m ///usr/share/kata-containers
 Line 570: install_path=/usr/share/kata-containers
 Line 572: suffix=
 Line 573: [[ '' != '' ]]
 Line 577: [[ '' != '' ]]
 Line 579: [[ '' != '' ]]
 Line 586: vmlinuz=vmlinuz-6.12.47-182
 Line 587: vmlinux=vmlinux-6.12.47-182
 Line 589: '[' -e arch/arm64/boot/bzImage ']'
 Line 591: '[' -e arch/arm64/boot/Image.gz ']'
 Line 592: bzImage=arch/arm64/boot/Image.gz
 Line 598: '[' arm64 = powerpc ']'
 Line 601: install --mode 0644 -D arch/arm64/boot/Image.gz /usr/share/kata-containers/vmlinuz-6.12.47-182
 Line 605: '[' arm64 = arm64 ']'
 Line 606: install --mode 0644 -D arch/arm64/boot/Image /usr/share/kata-containers/vmlinux-6.12.47-182
 Line 613: install --mode 0644 -D ./.config /usr/share/kata-containers/config-6.12.47-182
 Line 615: ln -sf vmlinuz-6.12.47-182 /usr/share/kata-containers/vmlinuz.container
 Line 616: ln -sf vmlinux-6.12.47-182 /usr/share/kata-containers/vmlinux.container
 Line 617: ls -la /usr/share/kata-containers/vmlinux.container
lrwxrwxrwx 1 root root 19 Feb 27 18:35 /usr/share/kata-containers/vmlinux.container -> vmlinux-6.12.47-182
 Line 618: ls -la /usr/share/kata-containers/vmlinuz.container
lrwxrwxrwx 1 root root 19 Feb 27 18:35 /usr/share/kata-containers/vmlinuz.container -> vmlinuz-6.12.47-182
 Line 619: popd

 ### nerdctl 실행을 위한 설정 파일 변경 및 nerdctl 설치
 #### ls /opt/cni/bin/
 #### ls /usr/lib/cni/
 #### containerd config dump | grep -i cni
 #### crictl info 2>/dev/null | grep -i cni
 bandwidth  dhcp   firewall  host-device  ipvlan    macvlan  ptp  static  vlan
bridge     dummy  flannel   host-local   loopback  portmap  sbr  tuning  vrf
ls: cannot access '/usr/lib/cni/': No such file or directory
    [plugins."io.containerd.grpc.v1.cri".cni]
      bin_dir = "/opt/cni/bin"
      conf_dir = "/etc/cni/net.d"
        cni_conf_dir = ""
        cni_max_conf_num = 0
          cni_conf_dir = ""
          cni_max_conf_num = 0
        cni_conf_dir = ""
        cni_max_conf_num = 0
  "cniconfig": {
      "/opt/cni/bin"
    "PluginConfDir": "/etc/cni/net.d",
          "Name": "cni-loopback",
          "CNIVersion": "0.3.1",
          "Source": "{\n\"cniVersion\": \"0.3.1\",\n\"name\": \"cni-loopback\",\n\"plugins\": [{\n  \"type\": \"loopback\"\n}]\n}"
          "CNIVersion": "0.3.1",
          "Source": "{\n  \"name\": \"cbr0\",\n  \"cniVersion\": \"0.3.1\",\n  \"plugins\": [\n    {\n      \"type\": \"flannel\",\n      \"delegate\": {\n        \"hairpinMode\": true,\n        \"isDefaultGateway\": true\n      }\n    },\n    {\n      \"type\": \"portmap\",\n      \"capabilities\": {\n        \"portMappings\": true\n      }\n    }\n  ]\n}\n"
        "cniConfDir": "",
        "cniMaxConfNum": 0,
        "cniConfDir": "",
        "cniMaxConfNum": 0,
          "cniConfDir": "",
          "cniMaxConfNum": 0,
    "cni": {
      "binDir": "/opt/cni/bin",
      "confDir": "/etc/cni/net.d",
  "lastCNILoadStatus": "OK",
  "lastCNILoadStatus.default": "OK"

  #### /opt/cni/bin/bridge 2>&1 | head -3
  #### ls -la /opt/cni/bin/ | head -3
  #### dpkg -l | grep -i cni
  CNI bridge plugin v1.2.0
CNI protocol versions supported: 0.1.0, 0.2.0, 0.3.0, 0.3.1, 0.4.0, 1.0.0
total 71108
drwxr-xr-x 2 root root    4096 Jan 30 18:01 .
drwxr-xr-x 3 root root    4096 Nov  4 13:52 ..
ii  kubernetes-cni                                1.2.0-2.1

### containerd 설정 파일 변경 (이미지대로 수정 - kata 부분 추가)
#### sudo cp /etc/containerd/config.toml /etc/containerd/config.toml.bak
#### sudo nano /etc/containerd/config.toml
<img width="1171" height="953" alt="image" src="https://github.com/user-attachments/assets/6a7f7ad4-ff15-4395-9670-d9d852145df5" />

#### sudo -i
#### cat > /etc/cni/net.d/10-mynet.conf << 'EOF'
#### {
####     "cniVersion": "0.2.0",
####     "name": "mynet",
####     "type": "bridge",
####     "bridge": "cni0",
####     "isGateway": true,
####     "ipMasq": true,
####     "ipam": {
####         "type": "host-local",
####         "subnet": "172.19.0.0/24",
####         "routes": [
####             { "dst": "0.0.0.0/0" }
####         ]
####     },
####     "dns": {
####         "nameservers": ["155.230.10.2"]
####     }
#### }
#### EOF

#### wget https://github.com/containerd/nerdctl/releases/download/v2.2.1/nerdctl-2.2.1-linux-arm64.tar.gz && tar xzvf nerdctl-2.2.1-linux-arm64.tar.gz && cp nerdctl /usr/local/bin/ && nerdctl --version

### 환경 동작 확인
#### sudo docker run -it --rm --runtime io.containerd.kata.v2 ubuntu:latest /bin/bash
