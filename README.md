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
# configuration written to /root/kata-containers/tools/packaging/kernel/configs/fragments/arm64/.config
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

#### cd ..
#### root@rpi4-desktop:~/kata-containers/tools/packaging/kernel# ./build-kernel.sh -a aarch64 -v 6.12.47 -f -d build && ./build-kernel.sh -a aarch64 -v 6.12.47 -d install
