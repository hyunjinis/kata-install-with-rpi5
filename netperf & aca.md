# Netperf Experiments with Kata Containers and ACA on Raspberry Pi

This document describes how to run network-performance experiments in a **Kata Containers microVM environment** and how to configure **ACA (Affinity-aware CPU Allocation)** by controlling the host-side Kata vCPU thread affinity.

> **Environment**
>
> - Kata Containers: `3.24.0`
> - Architecture: `aarch64`
> - Guest kernel: `Linux 6.12.47`
> - TCP congestion control: `CUBIC`
> - Container image: `jjong2/all:latest`
> - Netperf server: `192.168.0.5:12865`
> - Netperf test: `TCP_STREAM`
> - Message sizes: `64`, `128`, `256`, `512`, `1024 B`
> - Netperf duration: `300 s`
> - Monitoring interval: `10 s`
> - Number of monitoring samples: `13`

In the original container experiments, workload CPU affinity was controlled through the Pod cgroup.

In Kata Containers, the workload executes inside the guest VM. From the host perspective, guest workload execution is represented by the VMM's **vCPU thread**.

Therefore, ACA is applied by restricting the Kata vCPU thread to CPU cores excluding the cores used for NIC interrupt and softirq processing.

---

# 1. Create the Kata Experiment Container

The experiment image contains `netperf`, `vnstat`, `mpstat`, and `pidstat`.

Remove an existing experiment container if necessary.

**Command**

```bash
sudo nerdctl rm -f \
  kata-test \
  2>/dev/null || true
```

Create a persistent Kata container.

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

# 2. Verify the Kata Guest Environment

## 2.1 Check the guest kernel

```bash
sudo nerdctl exec \
  kata-test \
  uname -r
```

Expected:

```text
6.12.47
```

---

## 2.2 Check the actual guest-kernel image

Because both the baseline and Pre-GSO kernels report `6.12.47`, `uname -r` alone cannot distinguish them.

Check the kernel selected by Kata:

```bash
sudo kata-runtime env \
  | grep -A5 '\[Kernel\]'
```

For the baseline CUBIC kernel:

```text
[Kernel]

  Path = "/opt/kata/share/kata-containers/vmlinux-6.12.47-202"
```

For the Pre-GSO CUBIC kernel:

```text
[Kernel]

  Path = "/opt/kata/share/kata-containers/vmlinux-6.12.47-custom-cubic"
```

---

## 2.3 Verify CUBIC

Check the active TCP congestion-control algorithm.

```bash
sudo nerdctl exec \
  kata-test \
  sysctl net.ipv4.tcp_congestion_control
```

Expected:

```text
net.ipv4.tcp_congestion_control = cubic
```

Check all available congestion-control algorithms.

```bash
sudo nerdctl exec \
  kata-test \
  sysctl net.ipv4.tcp_available_congestion_control
```

Observed:

```text
net.ipv4.tcp_available_congestion_control = reno bbr cubic
```

---

## 2.4 Check required experiment tools

```bash
sudo nerdctl exec kata-test which netperf
sudo nerdctl exec kata-test which vnstat
sudo nerdctl exec kata-test which mpstat
sudo nerdctl exec kata-test which pidstat
```

Expected:

```text
/usr/bin/netperf
/usr/bin/vnstat
/usr/bin/mpstat
/usr/bin/pidstat
```

---

# 3. Find the Kata QEMU Process

ACA must be applied to the host-side vCPU execution thread of the Kata microVM.

Find the QEMU process.

```bash
pgrep -af qemu
```

<details>
<summary><strong>Show actual terminal output</strong></summary>

```text
399594 /opt/kata/bin/qemu-system-aarch64 \
-name sandbox-95d758e36e93141e3ee569c653f485b7a2589047975dbac9e71327e58fb5b41b \
-uuid 460d3a75-88dc-4441-9fa3-698e7da2f094 \
-machine virt,usb=off,accel=kvm,gic-version=host,nvdimm=on \
-cpu host,pmu=off \
...
-kernel /opt/kata/share/kata-containers/vmlinux-6.12.47-custom-cubic \
...
-smp 1,cores=1,threads=1,sockets=4,maxcpus=4
```

</details>

The important information is:

```text
QEMU PID = 399594

-smp 1
```

`-smp 1` means that the current Kata VM is running with one active vCPU.

> The QEMU PID changes whenever the Kata microVM is recreated.
>
> Do not permanently hard-code `399594`.

A convenient command is:

```bash
QEMU_PID=$(pgrep -f \
  '^/opt/kata/bin/qemu-system-aarch64 ' \
  | head -n 1)

echo "QEMU_PID=$QEMU_PID"
```

---

# 4. Inspect QEMU Threads

Inspect all threads belonging to the QEMU process.

```bash
ps -T \
  -p "$QEMU_PID" \
  -o pid,tid,psr,pcpu,comm
```

<details>
<summary><strong>Show actual terminal output</strong></summary>

```text
    PID     TID PSR %CPU COMMAND
 399594  399594   2  0.0 qemu-system-aar
 399594  399595   1  0.0 qemu-system-aar
 399594  399601   1  0.0 qemu-system-aar
 399594  399605   0 74.0 qemu-system-aar
 399594  399606   3  0.0 vhost-399594
 399594  399707   3 45.0 vhost-399594
```

</details>

In this example:

```text
QEMU PID       = 399594
vCPU TID       = 399605

vhost threads  = 399606
                 399707
```

The vCPU thread is the host-side execution entity corresponding to guest workload execution.

The `vhost-*` threads are host-side virtual-I/O processing threads and should not be treated as the guest workload vCPU thread.

---

# 5. Verify the vCPU Thread Using cgroups

To help distinguish the vCPU execution thread from QEMU overhead and vhost threads, inspect the cgroup of each thread.

```bash
QEMU_PID=$(pgrep -f \
  '^/opt/kata/bin/qemu-system-aarch64 ' \
  | head -n 1)

for task in /proc/$QEMU_PID/task/*; do

    tid=$(basename "$task")

    echo "================================"
    echo "TID: $tid"

    echo -n "NAME: "
    cat "$task/comm"

    echo "CGROUP:"
    cat "$task/cgroup"

done
```

Use this information together with:

```bash
ps -T \
  -p "$QEMU_PID" \
  -o pid,tid,psr,pcpu,comm
```

to identify the vCPU TID.

> Always identify the vCPU TID again after recreating the Kata VM.

---

# 6. ACA CPU Layout

The Raspberry Pi used in the experiment has four host CPU cores:

```text
CPU 0
CPU 1
CPU 2
CPU 3
```

An example ACA configuration is:

```text
CPU 0,1
    NIC IRQ
    network softirq processing

CPU 2,3
    Kata vCPU workload execution
```

Therefore:

```text
ACA OFF:
vCPU allowed CPUs = 0-3

ACA ON:
vCPU allowed CPUs = 2,3
```

The exact workload cores must match the network-interrupt affinity configuration used in the experiment.

---

# 7. Check NIC Interrupt Affinity

First inspect the host interrupts.

```bash
cat /proc/interrupts
```

The relevant network interrupt can also be searched using the interface or driver name.

```bash
grep -iE \
  'eth|genet|bcm' \
  /proc/interrupts
```

After identifying the IRQ number:

```bash
cat \
  /proc/irq/<IRQ>/smp_affinity_list
```

Example:

```text
0-1
```

This means that the corresponding NIC interrupt can run on CPUs 0 and 1.

The ACA workload CPU set should exclude these network-processing cores.

---

# 8. Disable ACA

ACA OFF allows the Kata vCPU thread to execute on all host CPUs.

For example:

```text
QEMU PID = 399594
vCPU TID = 399605
```

Set the vCPU affinity to all four host CPUs.

```bash
sudo taskset -pc \
  0-3 \
  399605
```

<details>
<summary><strong>Show actual terminal output</strong></summary>

```text
pid 399605's current affinity list: 1-3
pid 399605's new affinity list: 0-3
```

</details>

Verify:

```bash
taskset -pc \
  399605
```

Expected:

```text
pid 399605's current affinity list: 0-3
```

Also verify through `/proc`.

```bash
grep \
  Cpus_allowed_list \
  /proc/399594/task/399605/status
```

Expected:

```text
Cpus_allowed_list:    0-3
```

This configuration corresponds to:

```text
ACA = OFF
```

---

# 9. Enable ACA

Assume that the experimental CPU assignment is:

```text
NIC/network cores = CPU 0,1

Kata workload cores = CPU 2,3
```

Restrict the Kata vCPU thread to CPUs 2 and 3.

```bash
sudo taskset -pc \
  2,3 \
  399605
```

Expected:

```text
pid 399605's current affinity list: 0-3
pid 399605's new affinity list: 2,3
```

Verify:

```bash
taskset -pc \
  399605
```

Expected:

```text
pid 399605's current affinity list: 2,3
```

Also verify through `/proc`.

```bash
grep \
  Cpus_allowed_list \
  /proc/399594/task/399605/status
```

Expected:

```text
Cpus_allowed_list:    2-3
```

This configuration corresponds to:

```text
ACA = ON
```

---

# 10. Do Not Pin the Entire QEMU Process

Do not use the following command for the ACA experiment:

```bash
sudo taskset -apc \
  2,3 \
  <QEMU_PID>
```

The `-a` option changes the affinity of all QEMU threads.

This may include:

```text
vCPU threads
QEMU main thread
vhost threads
I/O-related threads
```

ACA is intended to isolate the workload execution context from the CPU cores responsible for network interrupt processing.

Therefore, only the identified vCPU execution thread should be controlled.

Correct:

```bash
sudo taskset -pc \
  2,3 \
  <VCPU_TID>
```

---

# 11. Verify Actual vCPU Execution During the Experiment

The `taskset` configuration specifies where the vCPU thread is allowed to execute.

To verify which host CPU the thread actually runs on during the experiment, use thread-level `pidstat`.

```bash
pidstat \
  -t \
  -p "$QEMU_PID" \
  1 10
```

The important fields are:

```text
TID
%CPU
CPU
```

For example:

```text
PID      TID      %usr   %system   %CPU   CPU   Command

399594   399605    ...     ...      75.0     2   qemu-system-aar
399594   399605    ...     ...      72.0     3   qemu-system-aar
```

With ACA enabled, the vCPU TID should only be observed on:

```text
CPU 2
CPU 3
```

and should not execute on:

```text
CPU 0
CPU 1
```

---

# 12. Measurements Collected During the Experiment

The following files are collected for each netperf message size.

| File | Description |
|---|---|
| `vnstat_guest.txt` | TX throughput and packet rate observed at the Kata guest interface |
| `mpstat_guest.txt` | Guest CPU utilization |
| `pidstat_netperf_guest.txt` | CPU utilization of the guest `netperf` process |
| `pidstat_vcpu_host.txt` | Host-side QEMU/vCPU thread CPU usage and CPU placement |
| `netperf.txt` | Netperf program output |
| `affinity_check.txt` | vCPU affinity configuration |
| `environment.txt` | Guest kernel, CCA, QEMU PID, vCPU TID, and other experiment information |

> Guest-interface PPS should not automatically be interpreted as physical wire PPS.
>
> GSO and the virtual network stack can cause guest-side packet counters to represent aggregated transmission units.

---

# 13. Manual netperf Test

Before running the full experiment, a short test can be executed.

```bash
sudo nerdctl exec \
  kata-test \
  netperf \
  -H 192.168.0.5 \
  -p 12865 \
  -l 30 \
  -- \
  -m 64
```

<details>
<summary><strong>Show actual terminal output</strong></summary>

```text
MIGRATED TCP STREAM TEST from 0.0.0.0 (0.0.0.0) port 0 AF_INET to 192.168.0.5 () port 0 AF_INET : demo

Recv   Send    Send
Socket Socket  Message  Elapsed
Size   Size    Size     Time     Throughput
bytes  bytes   bytes    secs.    10^6bits/sec

131072 16384      64    30.02       888.31
```

</details>

The `-m 64` option specifies a **64-byte send-message size** for netperf.

It does not mean that every physical Ethernet frame transmitted by the NIC is exactly 64 bytes.

---

# 14. Measure vnstat While netperf Is Running

`vnstat` must be executed while netperf traffic is active.

Incorrect sequence:

```text
netperf -l 30
        ↓
wait 30 s
        ↓
netperf terminates
        ↓
vnstat -tr 10
        ↓
0 traffic
```

Correct sequence:

```text
start netperf in background
        ↓
wait for traffic to stabilize
        ↓
measure vnstat while netperf is active
```

Example:

```bash
sudo nerdctl exec \
  kata-test \
  netperf \
  -H 192.168.0.5 \
  -p 12865 \
  -l 30 \
  -- \
  -m 64 \
  > /tmp/netperf64.txt 2>&1 &
```

Wait for traffic to stabilize.

```bash
sleep 2
```

Measure guest traffic.

```bash
sudo nerdctl exec \
  kata-test \
  vnstat \
  -i eth0 \
  -tr 10
```

---

# 15. Experimental Measurement Structure

The Kata experiment preserves the measurement structure used in the previous container experiment.

For each message size:

```text
1. Start one TCP_STREAM netperf flow
   netperf -l 300

2. Wait 1 second

3. Repeat 13 times:

   - Measure guest TX throughput/PPS for 10 seconds
   - Measure netperf process CPU usage for 10 seconds
   - Measure guest CPU usage for 10 seconds
   - Measure host QEMU/vCPU thread usage for 10 seconds

4. Wait approximately 3 seconds between samples

5. Stop netperf

6. Wait 10 seconds

7. Continue with the next message size
```

Message sizes:

```text
64 B
128 B
256 B
512 B
1024 B
```

---

# 16. Full Master-Side Experiment Script

The Kata microVM is running on the Raspberry Pi worker.

When this script is executed on the master machine, commands for the Kata container must therefore be executed through SSH on the worker.

Create:

```bash
nano kata_netperf.sh
```

Paste the following script.

```bash
#!/bin/bash

set -u

# ============================================================
# Experiment configuration
# ============================================================

PKTS=(
    64
    128
    256
    512
    1024
)

CONTAINER_NAME="kata-test"

SERVER_IP="192.168.0.5"
SERVER_PORT="12865"

WORKER_USER="rpi3"
WORKER_IP="192.168.0.X"

SSH_PASS="0000"
SUDO_PASS="0000"

NUM_SAMPLES=13
NETPERF_TIME=300

# ============================================================
# ACA configuration
# ============================================================

# ACA_MODE:
#
#   off : vCPU can execute on all host CPU cores.
#   on  : vCPU is restricted to workload cores.
#
ACA_MODE="off"

ALL_CORES="0-3"

# Example:
# Network processing = CPU 0,1
# Workload execution = CPU 2,3
#
ACA_CORES="2,3"

# IMPORTANT:
#
# The vCPU TID changes whenever the Kata VM is recreated.
#
# Run:
#
#   pgrep -af qemu
#   ps -T -p <QEMU_PID> -o pid,tid,psr,pcpu,comm
#
# and update this value before the experiment.
#
VCPU_TID="<VCPU_TID>"

# ============================================================
# SSH configuration
# ============================================================

SSH_CMD=(
    sshpass
    -p "$SSH_PASS"
    ssh
    -o StrictHostKeyChecking=no
    "${WORKER_USER}@${WORKER_IP}"
)

remote()
{
    "${SSH_CMD[@]}" "$1"
}

# ============================================================
# Pre-check
# ============================================================

echo "========================================"
echo "Kata netperf experiment"
echo "========================================"

echo
echo "[1] Check Kata container"

remote \
"echo '$SUDO_PASS' | sudo -S -p '' \
nerdctl ps"

echo
echo "[2] Check guest kernel"

remote \
"echo '$SUDO_PASS' | sudo -S -p '' \
nerdctl exec '$CONTAINER_NAME' \
uname -r"

echo
echo "[3] Check guest TCP congestion control"

CCA=$(remote \
"echo '$SUDO_PASS' | sudo -S -p '' \
nerdctl exec '$CONTAINER_NAME' \
sysctl -n net.ipv4.tcp_congestion_control")

echo "CCA=$CCA"

if [ "$CCA" != "cubic" ]; then

    echo
    echo "ERROR:"
    echo "TCP congestion control is not CUBIC."

    exit 1
fi

# ============================================================
# Find QEMU PID
# ============================================================

QEMU_PID=$(remote \
"pgrep -f '^/opt/kata/bin/qemu-system-aarch64 ' \
| head -n 1")

if [ -z "$QEMU_PID" ]; then

    echo
    echo "ERROR:"
    echo "Kata QEMU process was not found."

    exit 1
fi

echo
echo "QEMU_PID=$QEMU_PID"
echo "VCPU_TID=$VCPU_TID"

# ============================================================
# Verify the vCPU TID
# ============================================================

remote \
"test -d /proc/$QEMU_PID/task/$VCPU_TID"

if [ "$?" -ne 0 ]; then

    echo
    echo "ERROR:"
    echo "vCPU TID $VCPU_TID does not belong to QEMU PID $QEMU_PID."
    echo
    echo "Check QEMU threads using:"
    echo
    echo "ps -T -p $QEMU_PID -o pid,tid,psr,pcpu,comm"

    exit 1
fi

# ============================================================
# Configure ACA
# ============================================================

echo
echo "[4] Configure ACA"

if [ "$ACA_MODE" = "on" ]; then

    echo "ACA = ON"
    echo "vCPU allowed CPUs = $ACA_CORES"

    remote \
    "echo '$SUDO_PASS' | sudo -S -p '' \
    taskset -pc '$ACA_CORES' '$VCPU_TID'"

elif [ "$ACA_MODE" = "off" ]; then

    echo "ACA = OFF"
    echo "vCPU allowed CPUs = $ALL_CORES"

    remote \
    "echo '$SUDO_PASS' | sudo -S -p '' \
    taskset -pc '$ALL_CORES' '$VCPU_TID'"

else

    echo
    echo "ERROR:"
    echo "ACA_MODE must be 'on' or 'off'."

    exit 1
fi

echo
echo "[5] Verify vCPU affinity"

remote \
"taskset -pc '$VCPU_TID'"

remote \
"grep Cpus_allowed_list \
/proc/$QEMU_PID/task/$VCPU_TID/status"

echo
echo "========================================"
echo "Starting experiment"
echo "========================================"

# ============================================================
# Run experiments
# ============================================================

for pkt in "${PKTS[@]}"
do

    RESULT_DIR="p${pkt}_kata_${ACA_MODE}"

    mkdir -p \
    "$RESULT_DIR"

    echo
    echo "========================================"
    echo "Message size : ${pkt} B"
    echo "ACA mode     : ${ACA_MODE}"
    echo "Result dir   : ${RESULT_DIR}"
    echo "========================================"

    # --------------------------------------------------------
    # Save experiment environment
    # --------------------------------------------------------

    {
        echo "Message size = ${pkt} B"
        echo "ACA mode = ${ACA_MODE}"
        echo "QEMU PID = ${QEMU_PID}"
        echo "vCPU TID = ${VCPU_TID}"

        echo
        echo "=== Guest kernel ==="

        remote \
        "echo '$SUDO_PASS' | sudo -S -p '' \
        nerdctl exec '$CONTAINER_NAME' \
        uname -r"

        echo
        echo "=== TCP congestion control ==="

        remote \
        "echo '$SUDO_PASS' | sudo -S -p '' \
        nerdctl exec '$CONTAINER_NAME' \
        sysctl net.ipv4.tcp_congestion_control"

        echo
        echo "=== Available congestion controls ==="

        remote \
        "echo '$SUDO_PASS' | sudo -S -p '' \
        nerdctl exec '$CONTAINER_NAME' \
        sysctl net.ipv4.tcp_available_congestion_control"

        echo
        echo "=== QEMU threads ==="

        remote \
        "ps -T \
        -p '$QEMU_PID' \
        -o pid,tid,psr,pcpu,comm"

    } > "$RESULT_DIR/environment.txt"

    # --------------------------------------------------------
    # Save vCPU affinity
    # --------------------------------------------------------

    {
        echo "=== taskset ==="

        remote \
        "taskset -pc '$VCPU_TID'"

        echo
        echo "=== /proc status ==="

        remote \
        "grep Cpus_allowed_list \
        /proc/$QEMU_PID/task/$VCPU_TID/status"

    } > "$RESULT_DIR/affinity_check.txt"

    # --------------------------------------------------------
    # Start netperf in the Kata guest
    # --------------------------------------------------------

    remote \
    "echo '$SUDO_PASS' | sudo -S -p '' \
    nerdctl exec '$CONTAINER_NAME' \
    sh -lc \
    'nice -n 0 \
    taskset -c 0 \
    netperf \
    -H $SERVER_IP \
    -p $SERVER_PORT \
    -l $NETPERF_TIME \
    -- \
    -m $pkt'" \
    >> "$RESULT_DIR/netperf.txt" \
    2>&1 &

    NETPERF_SSH_PID=$!

    # Warm-up
    sleep 1

    # --------------------------------------------------------
    # Monitoring loop
    # --------------------------------------------------------

    for sample in $(seq 1 "$NUM_SAMPLES")
    do

        echo \
        "pkt=${pkt} sample=${sample}/${NUM_SAMPLES}"

        # ----------------------------------------------------
        # Guest throughput and packet rate
        # ----------------------------------------------------

        remote \
        "echo '$SUDO_PASS' | sudo -S -p '' \
        nerdctl exec '$CONTAINER_NAME' \
        taskset -c 0 \
        vnstat -tr 10" \
        | awk '/tx/' \
        | awk '{print $2,$4}' \
        >> "$RESULT_DIR/vnstat_guest.txt" &

        VNSTAT_PID=$!

        # ----------------------------------------------------
        # Guest netperf process CPU usage
        # ----------------------------------------------------

        remote \
        "echo '$SUDO_PASS' | sudo -S -p '' \
        nerdctl exec '$CONTAINER_NAME' \
        pidstat -G netperf 1 10" \
        >> "$RESULT_DIR/pidstat_netperf_guest.txt" &

        NETPERF_PIDSTAT_PID=$!

        # ----------------------------------------------------
        # Guest CPU utilization
        # ----------------------------------------------------

        remote \
        "echo '$SUDO_PASS' | sudo -S -p '' \
        nerdctl exec '$CONTAINER_NAME' \
        taskset -c 0 \
        mpstat -P ALL 10 1" \
        | awk '/Average/' \
        >> "$RESULT_DIR/mpstat_guest.txt" &

        MPSTAT_PID=$!

        # ----------------------------------------------------
        # Host QEMU / vCPU thread monitoring
        # ----------------------------------------------------

        remote \
        "pidstat \
        -t \
        -p '$QEMU_PID' \
        1 10" \
        >> "$RESULT_DIR/pidstat_vcpu_host.txt" &

        HOST_PIDSTAT_PID=$!

        # ----------------------------------------------------
        # Host CPU utilization
        # ----------------------------------------------------

        remote \
        "mpstat -P ALL 10 1" \
        | awk '/Average/' \
        >> "$RESULT_DIR/mpstat_host.txt" &

        HOST_MPSTAT_PID=$!

        # ----------------------------------------------------
        # Wait for the 10-second monitoring interval
        # ----------------------------------------------------

        wait "$VNSTAT_PID"
        wait "$NETPERF_PIDSTAT_PID"
        wait "$MPSTAT_PID"
        wait "$HOST_PIDSTAT_PID"
        wait "$HOST_MPSTAT_PID"

        sleep 3

    done

    # --------------------------------------------------------
    # Stop netperf
    # --------------------------------------------------------

    remote \
    "echo '$SUDO_PASS' | sudo -S -p '' \
    nerdctl exec '$CONTAINER_NAME' \
    killall netperf \
    2>/dev/null || true"

    wait "$NETPERF_SSH_PID" \
    2>/dev/null || true

    sleep 10

done

echo
echo "========================================"
echo "Experiment completed"
echo "========================================"
```

---

# 17. Configure the Experiment Script

Before executing the script, update:

```bash
WORKER_USER="rpi3"

WORKER_IP="192.168.0.X"

SSH_PASS="0000"

SUDO_PASS="0000"

VCPU_TID="<VCPU_TID>"
```

Check the Raspberry Pi worker IP using:

```bash
hostname -I
```

Determine the current QEMU PID:

```bash
pgrep -af qemu
```

Then inspect its threads.

```bash
QEMU_PID=<QEMU_PID>

ps -T \
  -p "$QEMU_PID" \
  -o pid,tid,psr,pcpu,comm
```

Set:

```bash
VCPU_TID="<VCPU_TID>"
```

to the identified vCPU execution thread.

---

# 18. Run with ACA Disabled

Set:

```bash
ACA_MODE="off"
```

The script applies:

```bash
taskset -pc \
  0-3 \
  <VCPU_TID>
```

The generated result directories are:

```text
p64_kata_off/
p128_kata_off/
p256_kata_off/
p512_kata_off/
p1024_kata_off/
```

---

# 19. Run with ACA Enabled

Set:

```bash
ACA_MODE="on"
```

The script applies:

```bash
taskset -pc \
  2,3 \
  <VCPU_TID>
```

The generated result directories are:

```text
p64_kata_on/
p128_kata_on/
p256_kata_on/
p512_kata_on/
p1024_kata_on/
```

---

# 20. Make the Script Executable

```bash
chmod +x \
  kata_netperf.sh
```

Run:

```bash
./kata_netperf.sh
```

---

# 21. Result Directory Structure

For example:

```text
p64_kata_on/
├── affinity_check.txt
├── environment.txt
├── mpstat_guest.txt
├── netperf.txt
├── pidstat_netperf_guest.txt
├── pidstat_vcpu_host.txt
└── vnstat_guest.txt
```

The same structure is created for:

```text
64 B
128 B
256 B
512 B
1024 B
```

---

# 22. `vnstat_guest.txt`

The experiment uses:

```bash
vnstat -tr 10
```

and extracts:

```bash
awk '/tx/' \
  | awk '{print $2,$4}'
```

An example result with Pre-GSO and ACA enabled was:

```text
937.71 4505
939.25 4724
938.96 4674
936.92 4492
940.96 4164
940.22 4934
937.69 4432
940.42 4647
```

The first column represents the TX throughput reported by `vnstat`.

The second column represents the TX packet-rate value reported at the guest interface.

> The packet rate measured at the Kata guest interface is not necessarily equal to the physical Ethernet frame rate.
>
> GSO and virtual networking may cause one guest-side TX unit to represent a larger aggregated packet before segmentation at a lower layer.

---

# 23. Example Result with ACA Disabled

With the Pre-GSO guest kernel active and ACA disabled:

```text
635.74 48838
853.63 19866
382.18 35701
534.18 45207
408.72 37656
388.72 36055
832.79 61113
384.31 35815
730.07 42997
```

The vCPU affinity was changed using:

```bash
sudo taskset -pc \
  0,1,2,3 \
  399605
```

Actual output:

```text
pid 399605's current affinity list: 1-3
pid 399605's new affinity list: 0-3
```

This allows the Kata workload vCPU to execute on the network-processing cores.

---

# 24. Example Result with ACA Enabled

With the same Pre-GSO guest kernel and ACA enabled:

```text
937.71 4505
939.25 4724
938.96 4674
936.92 4492
940.96 4164
940.22 4934
937.69 4432
940.42 4647
```

The vCPU affinity was configured as:

```bash
sudo taskset -pc \
  2,3 \
  <VCPU_TID>
```

This separates the host-side guest workload execution from the network-processing CPU cores.

---

# 25. Verify the vCPU Affinity from the Result Files

The configured CPU affinity is stored in:

```text
affinity_check.txt
```

Example:

```text
=== taskset ===

pid 399605's current affinity list: 2,3

=== /proc status ===

Cpus_allowed_list:    2-3
```

Runtime host-CPU placement is stored in:

```text
pidstat_vcpu_host.txt
```

For example:

```bash
grep \
  399605 \
  p64_kata_on/pidstat_vcpu_host.txt
```

With ACA enabled, the `CPU` column for the vCPU TID should only show:

```text
2
3
```

and should not show:

```text
0
1
```

---

# 26. `pidstat_netperf_guest.txt` and `pidstat_vcpu_host.txt`

These files measure different layers.

## `pidstat_netperf_guest.txt`

This file measures the guest-side application:

```text
netperf
    ↓
Kata guest kernel
```

It reports the CPU usage of the netperf process inside the microVM.

If the VM has one vCPU, the guest application will generally execute on:

```text
guest CPU 0
```

This does not indicate which physical host CPU executes the guest vCPU.

---

## `pidstat_vcpu_host.txt`

This file measures the host-side execution context:

```text
Guest netperf
      ↓
Guest vCPU
      ↓
QEMU/KVM vCPU thread
      ↓
Host physical CPU
```

Therefore, `pidstat_vcpu_host.txt` is the relevant file for verifying ACA host-side CPU isolation.

---

# 27. QEMU PID and vCPU TID Change after VM Recreation

For one experiment:

```text
QEMU PID = 399594
vCPU TID = 399605
```

These values apply only to that particular Kata microVM.

After:

```bash
sudo nerdctl rm -f \
  kata-test
```

and recreating the VM:

```bash
sudo nerdctl run -d \
  --name kata-test \
  --runtime io.containerd.kata.v2 \
  jjong2/all:latest \
  sleep infinity
```

the QEMU PID and vCPU TID change.

Therefore, before each new environment setup, run:

```bash
pgrep -af qemu
```

and:

```bash
ps -T \
  -p <QEMU_PID> \
  -o pid,tid,psr,pcpu,comm
```

again.

Do not reuse an old TID such as `399605` after recreating the VM.

---

# 28. Recommended Experimental Order

All experiments use CUBIC.

The experiment can be divided into four configurations.

| Configuration | Guest kernel | Pre-GSO | ACA | CCA |
|---|---|---:|---:|---|
| Baseline | `vmlinux-6.12.47-202` | OFF | OFF | CUBIC |
| ACA | `vmlinux-6.12.47-202` | OFF | ON | CUBIC |
| Pre-GSO | `vmlinux-6.12.47-custom-cubic` | ON | OFF | CUBIC |
| ACA + Pre-GSO | `vmlinux-6.12.47-custom-cubic` | ON | ON | CUBIC |

Recommended sequence:

```text
1. Baseline
   Kernel = vmlinux-6.12.47-202
   ACA    = OFF
   vCPU   = CPUs 0-3

2. ACA
   Kernel = vmlinux-6.12.47-202
   ACA    = ON
   vCPU   = workload CPU set

3. Pre-GSO
   Kernel = vmlinux-6.12.47-custom-cubic
   ACA    = OFF
   vCPU   = CPUs 0-3

4. ACA + Pre-GSO
   Kernel = vmlinux-6.12.47-custom-cubic
   ACA    = ON
   vCPU   = workload CPU set
```

---

# 29. Pre-Experiment Checklist

Before each experiment, verify:

```text
[ ] Correct guest kernel is selected
[ ] Kata VM was recreated after changing the kernel
[ ] guest uname -r = 6.12.47
[ ] tcp_congestion_control = cubic
[ ] netperf is installed
[ ] vnstat is installed
[ ] mpstat is installed
[ ] pidstat is installed
[ ] only the intended Kata experiment VM is running
[ ] current QEMU PID is identified
[ ] current vCPU TID is identified
[ ] network IRQ CPU assignment is known
[ ] ACA affinity is correctly configured
[ ] Cpus_allowed_list is verified
[ ] netperf server 192.168.0.5:12865 is running
```

---

# 30. Quick ACA Commands

## Find QEMU PID

```bash
QEMU_PID=$(pgrep -f \
  '^/opt/kata/bin/qemu-system-aarch64 ' \
  | head -n 1)

echo "$QEMU_PID"
```

## Inspect QEMU threads

```bash
ps -T \
  -p "$QEMU_PID" \
  -o pid,tid,psr,pcpu,comm
```

## ACA OFF

```bash
sudo taskset -pc \
  0-3 \
  <VCPU_TID>
```

## ACA ON

```bash
sudo taskset -pc \
  2,3 \
  <VCPU_TID>
```

## Verify affinity

```bash
taskset -pc \
  <VCPU_TID>
```

```bash
grep \
  Cpus_allowed_list \
  /proc/$QEMU_PID/task/<VCPU_TID>/status
```

## Monitor actual host CPU placement

```bash
pidstat \
  -t \
  -p "$QEMU_PID" \
  1 10
```

---

# 31. Summary

The host-side execution structure of a standard container is:

```text
Container workload process
        ↓
Host scheduler
        ↓
Host physical CPU
```

For Kata Containers:

```text
Guest workload
        ↓
Guest scheduler
        ↓
Guest vCPU
        ↓
QEMU/KVM vCPU thread
        ↓
Host scheduler
        ↓
Host physical CPU
```

Therefore, ACA in the Kata environment controls the host-side **vCPU execution thread** instead of directly controlling the guest application process.

The experiment collects:

```text
Guest network throughput / PPS
Guest CPU utilization
Guest netperf CPU utilization
Host QEMU/vCPU utilization
Host physical CPU placement
```

while preserving the same netperf workload and sampling methodology used for the previous container experiments.
