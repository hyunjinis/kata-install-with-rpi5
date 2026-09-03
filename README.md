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

sudo modprobe vhost
sudo modprobe vhost_net
sudo modprobe vhost_vsock

lsmod | grep -E 'vhost|vsock|tap'
vhost_vsock            24576  0
vmw_vsock_virtio_transport_common    53248  1 vhost_vsock
vsock                  61440  2 vmw_vsock_virtio_transport_common,vhost_vsock
vhost_net              32768  0
tun                    61440  1 vhost_net
tap                    36864  1 vhost_net
vhost                  69632  2 vhost_vsock,vhost_net
vhost_iotlb            16384  1 vhost

kata-runtime --version
kata-runtime  : 3.24.0
   commit   : c7d0c270ee7dfaa6d978e6e07b99dabdaf2b9fda
   OCI specs: 1.2.1
   
sudo kata-runtime check
WARN[0000] Not running network checks as super user      arch=arm64 name=kata-runtime pid=1800336 source=runtime
System is capable of running Kata Containers
System can currently create Kata Containers

sudo apt install -y flex bison libelf-dev libncurses-dev

wget https://go.dev/dl/go1.26.0.linux-arm64.tar.gz

sudo rm -rf /usr/local/go
sudo tar -C /usr/local -xzf go1.26.0.linux-arm64.tar.gz

echo 'export PATH=$PATH:/usr/local/go/bin' >> ~/.bashrc
source ~/.bashrc

go version
