# kata-install-with-rpi5

## Environment Setup
#### sudo apt install && sudo apt update && wget https://github.com/kata-containers/kata-containers/releases/download/3.24.0/kata-static-3.24.0-arm64.tar.zst && sudo tar -xvf kata-static-3.24.0-arm64.tar.zst -C / && rm kata-static-3.24.0-arm64.tar.zst && ln -s /opt/kata/bin/kata-runtime /usr/local/bin && ln -s /opt/kata/bin/containerd-shim-kata-v2 /usr/local/bin && ln -s /opt/kata/bin/kata-collect-data.sh /usr/local/bin
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
