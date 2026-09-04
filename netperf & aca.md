Netperf Experiments with Kata Containers and ACA on Raspberry Pi

This document describes how to run the network-performance experiments in a Kata Containers microVM environment and how to configure ACA (Affinity-aware CPU Allocation) by controlling the host-side Kata vCPU thread affinity.

The experiment uses:

Kata Containers       3.24.0
Architecture          aarch64
Guest kernel          Linux 6.12.47
TCP CCA               CUBIC
Container image       jjong2/all:latest
Netperf server        192.168.0.5:12865
Netperf test          TCP_STREAM
Message sizes         64, 128, 256, 512, 1024 B
Netperf duration      300 s
Monitoring interval   10 s
Samples               13

In the original container experiments, workload CPU affinity was controlled through the Pod cgroup.

In Kata Containers, the workload executes inside the guest VM. From the host perspective, guest workload execution is represented by the VMM's vCPU thread.

Therefore, ACA is applied by restricting the Kata vCPU thread to CPU cores excluding the cores used for NIC interrupt and softirq processing.

1. Create the Kata Experiment Container

The experiment image contains netperf, vnstat, mpstat, and pidstat.

Remove an existing experiment container if necessary.

sudo nerdctl rm -f \
kata-test \
2>/dev/null || true

Create a persistent Kata container.

sudo nerdctl run -d \
--name kata-test \
--runtime io.containerd.kata.v2 \
jjong2/all:latest \
sleep infinity

Verify:

sudo nerdctl ps

Example:

CONTAINER ID    IMAGE                         COMMAND           STATUS    NAMES
xxxxxxxxxxxx    docker.io/jjong2/all:latest   "sleep infinity"  Up        kata-test
2. Verify the Kata Guest Environment
2.1 Check the guest kernel
sudo nerdctl exec \
kata-test \
uname -r

Expected:

6.12.47
2.2 Check the actual guest-kernel image

Because both the baseline and Pre-GSO kernels report 6.12.47, uname -r alone cannot distinguish them.

Check the kernel selected by Kata:

sudo kata-runtime env \
| grep -A5 '\[Kernel\]'

For the baseline CUBIC kernel:

[Kernel]

  Path = "/opt/kata/share/kata-containers/vmlinux-6.12.47-202"

For the Pre-GSO CUBIC kernel:

[Kernel]

  Path = "/opt/kata/share/kata-containers/vmlinux-6.12.47-custom-cubic"
2.3 Verify CUBIC

Check the active TCP congestion-control algorithm.

sudo nerdctl exec \
kata-test \
sysctl net.ipv4.tcp_congestion_control

Expected:

net.ipv4.tcp_congestion_control = cubic

Check all available CCAs.

sudo nerdctl exec \
kata-test \
sysctl net.ipv4.tcp_available_congestion_control

Observed:

net.ipv4.tcp_available_congestion_control = reno bbr cubic
2.4 Check required experiment tools
sudo nerdctl exec \
kata-test \
which netperf

sudo nerdctl exec \
kata-test \
which vnstat

sudo nerdctl exec \
kata-test \
which mpstat

sudo nerdctl exec \
kata-test \
which pidstat

Expected:

/usr/bin/netperf
/usr/bin/vnstat
/usr/bin/mpstat
/usr/bin/pidstat
3. Find the Kata QEMU Process

ACA must be applied to the host-side vCPU execution thread of the Kata microVM.

Find the QEMU process.

pgrep -af \
qemu

<details> <summary><strong>Show actual terminal output</strong></summary>

399594 /opt/kata/bin/qemu-system-aarch64 \
-name sandbox-95d758e36e93141e3ee569c653f485b7a2589047975dbac9e71327e58fb5b41b \
-uuid 460d3a75-88dc-4441-9fa3-698e7da2f094 \
-machine virt,usb=off,accel=kvm,gic-version=host,nvdimm=on \
-cpu host,pmu=off \
...
-kernel /opt/kata/share/kata-containers/vmlinux-6.12.47-custom-cubic \
...
-smp 1,cores=1,threads=1,sockets=4,maxcpus=4

</details>

The important information is:

QEMU PID = 399594

-smp 1

-smp 1 means that the current Kata VM is running with one active vCPU.

The PID changes whenever the Kata microVM is recreated.

Never hard-code 399594 into a permanent experiment script.

A convenient command is:

QEMU_PID=$(pgrep -f \
'^/opt/kata/bin/qemu-system-aarch64 ' \
| head -n 1)

echo \
"QEMU_PID=$QEMU_PID"
4. Inspect QEMU Threads

Use the QEMU PID to inspect all QEMU threads.

ps -T \
-p "$QEMU_PID" \
-o pid,tid,psr,pcpu,comm

<details> <summary><strong>Show actual terminal output</strong></summary>

    PID     TID PSR %CPU COMMAND
 399594  399594   2  0.0 qemu-system-aar
 399594  399595   1  0.0 qemu-system-aar
 399594  399601   1  0.0 qemu-system-aar
 399594  399605   0 74.0 qemu-system-aar
 399594  399606   3  0.0 vhost-399594
 399594  399707   3 45.0 vhost-399594

</details>

In this example:

QEMU PID       = 399594
vCPU TID       = 399605

vhost threads  = 399606
                 399707

The vCPU thread is the host-side execution entity corresponding to guest workload execution.

The vhost-* threads are host-side virtual-I/O processing threads and should not be treated as the guest workload vCPU thread.

5. Verify the vCPU Thread Using cgroups

To distinguish the vCPU execution thread from QEMU overhead and vhost threads, inspect each thread's cgroup.

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

With the default Kata cgroup configuration, the vCPU thread is associated with the workload/sandbox CPU context while other VMM overhead threads may be placed separately.

Use this information together with:

ps -T \
-p "$QEMU_PID" \
-o pid,tid,psr,pcpu,comm

to identify the vCPU TID.

Always identify the vCPU TID again after recreating the Kata VM.

6. ACA CPU Layout

The Raspberry Pi used in the experiment has four host CPU cores:

CPU 0
CPU 1
CPU 2
CPU 3

An example ACA configuration is:

CPU 0,1
    NIC IRQ
    network softirq processing

CPU 2,3
    Kata vCPU workload execution

Therefore:

ACA OFF:
vCPU allowed CPUs = 0-3

ACA ON:
vCPU allowed CPUs = 2,3

The exact network-processing cores should match the IRQ-affinity configuration used in the experiment.

7. Check NIC Interrupt Affinity

First identify the IRQ associated with the physical network interface.

cat \
/proc/interrupts

or:

grep -i \
'eth\|genet\|bcm' \
/proc/interrupts

After identifying the relevant IRQ number:

cat \
/proc/irq/<IRQ>/smp_affinity_list

Example:

0-1

This means that the NIC interrupt is restricted to CPUs 0 and 1.

The ACA workload CPU set should therefore exclude these cores.

8. Disable ACA

ACA OFF allows the Kata vCPU thread to execute on all host CPUs.

Assume:

vCPU TID = 399605

Run:

sudo taskset -pc \
0-3 \
399605

<details> <summary><strong>Show actual terminal output</strong></summary>

pid 399605's current affinity list: 1-3
pid 399605's new affinity list: 0-3

</details>

Verify:

taskset -pc \
399605

Expected:

pid 399605's current affinity list: 0-3

Also check the Linux status file.

grep \
Cpus_allowed_list \
/proc/399594/task/399605/status

Expected:

Cpus_allowed_list:    0-3

This configuration corresponds to:

ACA = OFF
9. Enable ACA

Assume:

NIC/network cores = 0,1

Kata workload cores = 2,3

Apply the vCPU affinity.

sudo taskset -pc \
2,3 \
399605

Expected:

pid 399605's current affinity list: 0-3
pid 399605's new affinity list: 2,3

Verify:

taskset -pc \
399605

Expected:

pid 399605's current affinity list: 2,3

Also verify using /proc.

grep \
Cpus_allowed_list \
/proc/399594/task/399605/status

Expected:

Cpus_allowed_list:    2-3

This configuration corresponds to:

ACA = ON
10. Important: Do Not Pin the Entire QEMU Process

Do not use:

sudo taskset -apc \
2,3 \
<QEMU_PID>

for the ACA experiment.

The -a option changes the affinity of all QEMU threads, including:

vCPU threads
QEMU main thread
vhost threads
I/O-related threads

The original ACA mechanism isolates the workload execution context from network-processing cores.

Therefore, the corresponding Kata implementation should control the vCPU execution thread, rather than arbitrarily moving the entire VMM.

Correct:

sudo taskset -pc \
2,3 \
<VCPU_TID>
11. Verify Actual vCPU Execution During the Experiment

The affinity configuration defines where the thread is allowed to run.

To verify which physical CPU the vCPU thread actually uses during runtime, use thread-level pidstat.

pidstat \
-t \
-p "$QEMU_PID" \
1 10

The important columns are:

TID
%CPU
CPU

Example:

PID      TID      %usr   %system   %CPU   CPU   Command

399594   399605    ...     ...      75.0     2   qemu-system-aar
399594   399605    ...     ...      72.0     3   qemu-system-aar

With ACA enabled, the vCPU TID should only appear on:

CPU 2
CPU 3

and should not appear on:

CPU 0
CPU 1
12. Guest and Host Measurements

The following measurements are collected.

File	Measurement
vnstat_guest.txt	TX throughput and packet rate observed at the Kata guest interface
mpstat_guest.txt	Guest CPU utilization
pidstat_netperf_guest.txt	CPU utilization of the guest netperf process
pidstat_vcpu_host.txt	Host CPU utilization and CPU placement of QEMU/vCPU threads
netperf.txt	netperf program output
affinity_check.txt	vCPU affinity configuration
environment.txt	Kernel, CCA, QEMU PID, vCPU TID, etc.

Guest-interface PPS should not automatically be interpreted as physical wire PPS.

GSO and virtual networking may cause guest-side packet counters to represent aggregated transmission units.

13. Manual netperf Test

A short manual test can be run before starting the full experiment.

sudo nerdctl exec \
kata-test \
netperf \
-H 192.168.0.5 \
-p 12865 \
-l 30 \
-- \
-m 64

<details> <summary><strong>Show actual terminal output</strong></summary>

MIGRATED TCP STREAM TEST from 0.0.0.0 (0.0.0.0) port 0 AF_INET to 192.168.0.5 () port 0 AF_INET : demo

Recv   Send    Send
Socket Socket  Message  Elapsed
Size   Size    Size     Time     Throughput
bytes  bytes   bytes    secs.    10^6bits/sec

131072 16384      64    30.02       888.31

</details>

The -m 64 option specifies a 64-byte netperf send-message size.

It does not necessarily mean that every physical Ethernet frame is 64 bytes.

14. Test Guest vnstat Correctly

vnstat must be executed while netperf is running.

Incorrect:

run netperf for 30 s
        ↓
wait until netperf terminates
        ↓
run vnstat
        ↓
0 traffic

Correct:

start netperf
        ↓
netperf continues in background
        ↓
run vnstat while traffic is active

Example:

sudo nerdctl exec \
kata-test \
netperf \
-H 192.168.0.5 \
-p 12865 \
-l 30 \
-- \
-m 64 \
> /tmp/netperf64.txt 2>&1 &

Wait for the flow to stabilize.

sleep 2

Measure guest traffic.

sudo nerdctl exec \
kata-test \
vnstat \
-i eth0 \
-tr 10
15. Original Experimental Measurement Structure

The revised Kata experiment preserves the structure of the previous container experiment.

For each message size:

1. Start one TCP_STREAM netperf flow
   netperf -l 300

2. Wait 1 second

3. Repeat 13 times:
       - vnstat for 10 s
       - pidstat for 10 s
       - mpstat for 10 s

4. Wait approximately 3 s between monitoring windows

5. Stop netperf

6. Move to the next message size

Message sizes:

64 B
128 B
256 B
512 B
1024 B
16. Full Master-Side Kata Experiment Script

The Kata container runs on the Raspberry Pi worker.

Therefore, when the experiment script is executed from the Kubernetes/master machine, all nerdctl commands must be executed through SSH on the worker.

Create:

nano \
kata_netperf.sh

Paste:

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

# Set:
#
#   off : allow the vCPU thread on all host cores
#   on  : restrict the vCPU thread to workload cores
#
ACA_MODE="off"

ALL_CORES="0-3"
ACA_CORES="2,3"

# IMPORTANT:
# Update this after recreating the Kata VM.
#
# Example:
# VCPU_TID="399605"
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
"echo '$SUDO_PASS' | sudo -S -p '' nerdctl ps"

echo
echo "[2] Check guest kernel"

remote \
"echo '$SUDO_PASS' | sudo -S -p '' \
nerdctl exec '$CONTAINER_NAME' uname -r"

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

    echo "ERROR: Kata QEMU process was not found."
    exit 1

fi

echo
echo "QEMU_PID=$QEMU_PID"
echo "VCPU_TID=$VCPU_TID"

# ============================================================
# Verify that the supplied vCPU TID exists
# ============================================================

remote \
"test -d /proc/$QEMU_PID/task/$VCPU_TID"

if [ "$?" -ne 0 ]; then

    echo "ERROR:"
    echo "VCPU TID $VCPU_TID does not belong to QEMU PID $QEMU_PID."
    echo
    echo "Run:"
    echo "  ps -T -p $QEMU_PID -o pid,tid,psr,pcpu,comm"
    echo
    echo "and update VCPU_TID."
    exit 1

fi

# ============================================================
# Configure ACA
# ============================================================

echo
echo "[4] Configure ACA"

if [ "$ACA_MODE" = "on" ]; then

    echo "ACA = ON"
    echo "vCPU allowed cores = $ACA_CORES"

    remote \
    "echo '$SUDO_PASS' | sudo -S -p '' \
    taskset -pc '$ACA_CORES' '$VCPU_TID'"

elif [ "$ACA_MODE" = "off" ]; then

    echo "ACA = OFF"
    echo "vCPU allowed cores = $ALL_CORES"

    remote \
    "echo '$SUDO_PASS' | sudo -S -p '' \
    taskset -pc '$ALL_CORES' '$VCPU_TID'"

else

    echo "ERROR: ACA_MODE must be on or off."
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
    echo "Message size: ${pkt} B"
    echo "ACA mode    : ${ACA_MODE}"
    echo "Result dir  : ${RESULT_DIR}"
    echo "========================================"

    # --------------------------------------------------------
    # Save environment
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
        nerdctl exec '$CONTAINER_NAME' uname -r"

        echo
        echo "=== TCP congestion control ==="

        remote \
        "echo '$SUDO_PASS' | sudo -S -p '' \
        nerdctl exec '$CONTAINER_NAME' \
        sysctl net.ipv4.tcp_congestion_control"

        echo
        echo "=== Available CCA ==="

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

    } > \
    "$RESULT_DIR/environment.txt"

    # --------------------------------------------------------
    # Save affinity
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

    } > \
    "$RESULT_DIR/affinity_check.txt"

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
    # Monitoring
    # --------------------------------------------------------

    for sample in $(seq 1 "$NUM_SAMPLES")
    do

        echo \
        "pkt=${pkt} sample=${sample}/${NUM_SAMPLES}"

        # ----------------------------------------------------
        # Guest network throughput / PPS
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
        # Guest netperf process CPU
        # ----------------------------------------------------

        remote \
        "echo '$SUDO_PASS' | sudo -S -p '' \
        nerdctl exec '$CONTAINER_NAME' \
        pidstat -G netperf 1 10" \
        >> "$RESULT_DIR/pidstat_netperf_guest.txt" &

        NETPERF_PIDSTAT_PID=$!

        # ----------------------------------------------------
        # Guest CPU usage
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
        # Host QEMU/vCPU thread CPU placement
        # ----------------------------------------------------

        remote \
        "pidstat \
        -t \
        -p '$QEMU_PID' \
        1 10" \
        >> "$RESULT_DIR/pidstat_vcpu_host.txt" &

        HOST_PIDSTAT_PID=$!

        # ----------------------------------------------------
        # Wait for the four 10-second measurements
        # ----------------------------------------------------

        wait "$VNSTAT_PID"
        wait "$NETPERF_PIDSTAT_PID"
        wait "$MPSTAT_PID"
        wait "$HOST_PIDSTAT_PID"

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
17. Configure the Master-Side Script

The following variables must be updated before execution:

WORKER_USER="rpi3"

WORKER_IP="192.168.0.X"

SSH_PASS="0000"

SUDO_PASS="0000"

VCPU_TID="<VCPU_TID>"

Determine the worker IP on the Raspberry Pi:

hostname -I

Determine the current QEMU PID:

pgrep -af \
qemu

Then:

QEMU_PID=<QEMU_PID>

ps -T \
-p "$QEMU_PID" \
-o pid,tid,psr,pcpu,comm

Determine the vCPU TID and put it in:

VCPU_TID="<VCPU_TID>"
18. Select ACA OFF or ON
ACA OFF

Edit:

ACA_MODE="off"

The script automatically applies:

taskset -pc \
0-3 \
<VCPU_TID>

Result directories are created as:

p64_kata_off/
p128_kata_off/
p256_kata_off/
p512_kata_off/
p1024_kata_off/
ACA ON

Edit:

ACA_MODE="on"

The script automatically applies:

taskset -pc \
2,3 \
<VCPU_TID>

Result directories are created as:

p64_kata_on/
p128_kata_on/
p256_kata_on/
p512_kata_on/
p1024_kata_on/
19. Make the Script Executable
chmod +x \
kata_netperf.sh

Run:

./kata_netperf.sh
20. Result Directory Structure

For example:

p64_kata_on/
├── affinity_check.txt
├── environment.txt
├── mpstat_guest.txt
├── netperf.txt
├── pidstat_netperf_guest.txt
├── pidstat_vcpu_host.txt
└── vnstat_guest.txt

The same structure is generated for:

64 B
128 B
256 B
512 B
1024 B
21. vnstat_guest.txt

The script uses:

vnstat -tr 10

and extracts:

awk '/tx/' \
| awk '{print $2,$4}'

Example result:

937.71 4505
939.25 4724
938.96 4674
936.92 4492
940.96 4164
940.22 4934
937.69 4432
940.42 4647

The first value represents TX throughput and the second value represents the packet-rate value reported by the guest interface.

The guest-side packet rate is a virtual-interface statistic.

It should not automatically be interpreted as the physical Ethernet frame rate because GSO may aggregate multiple TCP sends into a larger guest-side transmission unit.

22. Example ACA-OFF Result

With Pre-GSO enabled and ACA disabled, an example 64-B result was:

635.74 48838
853.63 19866
382.18 35701
534.18 45207
408.72 37656
388.72 36055
832.79 61113
384.31 35815
730.07 42997

The vCPU affinity was configured as:

sudo taskset -pc \
0,1,2,3 \
399605

Actual output:

pid 399605's current affinity list: 1-3
pid 399605's new affinity list: 0-3

This configuration allows the Kata workload vCPU to contend with network-processing cores.

23. Example ACA-ON Result

With Pre-GSO enabled and the vCPU separated from the network-processing cores, the 64-B result was:

937.71 4505
939.25 4724
938.96 4674
936.92 4492
940.96 4164
940.22 4934
937.69 4432
940.42 4647

The corresponding affinity configuration is:

sudo taskset -pc \
2,3 \
<VCPU_TID>

This restricts guest workload execution to CPUs 2 and 3 while the network-processing cores are excluded from the workload CPU set.

24. Check Which Host CPUs the vCPU Actually Used

The affinity configuration is stored in:

affinity_check.txt

Example:

=== taskset ===
pid 399605's current affinity list: 2,3

=== /proc status ===
Cpus_allowed_list:    2-3

Runtime CPU placement is stored in:

pidstat_vcpu_host.txt

Search for the vCPU TID.

grep \
399605 \
p64_kata_on/pidstat_vcpu_host.txt

With ACA enabled, the CPU column should only contain the allowed workload CPUs.

For example:

CPU 2
CPU 3

and should not contain:

CPU 0
CPU 1
25. pidstat_netperf_guest.txt vs. pidstat_vcpu_host.txt

These two files measure different layers.

pidstat_netperf_guest.txt

This measures:

netperf process
inside Kata guest

It shows the CPU utilization of the guest workload.

If the Kata VM has one vCPU, netperf will generally execute on:

guest CPU 0

However, this does not reveal which host physical CPU executes that guest vCPU.

pidstat_vcpu_host.txt

This measures:

QEMU/vCPU execution
on the host

Therefore, this is the important file for verifying ACA.

The mapping is:

Guest netperf
      ↓
Guest vCPU
      ↓
QEMU vCPU thread
      ↓
Host physical CPU

ACA controls the final host-side CPU placement.

26. Important: QEMU and vCPU IDs Change after VM Recreation

For example, one experiment used:

QEMU PID = 399594
vCPU TID = 399605

These values are only valid for that particular Kata VM.

After:

sudo nerdctl rm -f \
kata-test

and:

sudo nerdctl run \
...

the new microVM will have different PID and TID values.

Therefore, before every new environment setup:

pgrep -af \
qemu

and:

ps -T \
-p <QEMU_PID> \
-o pid,tid,psr,pcpu,comm

must be checked again.

27. Recommended Experiment Order

To evaluate Baseline, ACA, Pre-GSO, and ACA + Pre-GSO under the same CUBIC configuration:

1. Baseline CUBIC kernel
   vmlinux-6.12.47-202

   ACA OFF
   vCPU affinity = 0-3


2. Baseline CUBIC kernel
   vmlinux-6.12.47-202

   ACA ON
   vCPU affinity = workload cores only


3. Pre-GSO CUBIC kernel
   vmlinux-6.12.47-custom-cubic

   ACA OFF
   vCPU affinity = 0-3


4. Pre-GSO CUBIC kernel
   vmlinux-6.12.47-custom-cubic

   ACA ON
   vCPU affinity = workload cores only

The resulting experimental matrix is:

Configuration	Guest kernel	Pre-GSO	ACA	CCA
Baseline	vmlinux-6.12.47-202	OFF	OFF	CUBIC
ACA	vmlinux-6.12.47-202	OFF	ON	CUBIC
Pre-GSO	vmlinux-6.12.47-custom-cubic	ON	OFF	CUBIC
ACA + Pre-GSO	vmlinux-6.12.47-custom-cubic	ON	ON	CUBIC
28. Pre-Experiment Checklist

Before starting each experiment, verify the following.

[ ] Correct guest kernel selected
[ ] Kata VM recreated after kernel change
[ ] guest uname -r = 6.12.47
[ ] tcp_congestion_control = cubic
[ ] netperf is installed
[ ] vnstat is installed
[ ] mpstat is installed
[ ] pidstat is installed
[ ] only one experiment Kata VM is running
[ ] current QEMU PID identified
[ ] current vCPU TID identified
[ ] NIC IRQ cores identified
[ ] ACA affinity configured
[ ] Cpus_allowed_list verified
[ ] netperf server 192.168.0.5:12865 is running
29. Quick ACA Configuration Commands
Find QEMU
QEMU_PID=$(pgrep -f \
'^/opt/kata/bin/qemu-system-aarch64 ' \
| head -n 1)

echo "$QEMU_PID"
Inspect threads
ps -T \
-p "$QEMU_PID" \
-o pid,tid,psr,pcpu,comm
ACA OFF
sudo taskset -pc \
0-3 \
<VCPU_TID>
ACA ON
sudo taskset -pc \
2,3 \
<VCPU_TID>
Verify
taskset -pc \
<VCPU_TID>
grep \
Cpus_allowed_list \
/proc/$QEMU_PID/task/<VCPU_TID>/status
Monitor actual execution
pidstat \
-t \
-p "$QEMU_PID" \
1 10
30. Summary

The Kata experiment maps the workload differently from a standard container.

Standard container:

Container process
        ↓
Host scheduler
        ↓
Host physical CPU

Kata Containers:

Guest workload
        ↓
Guest scheduler
        ↓
Guest vCPU
        ↓
Host QEMU/KVM vCPU thread
        ↓
Host scheduler
        ↓
Host physical CPU

Therefore, ACA in Kata is implemented by isolating the host-side vCPU execution thread from the CPU cores responsible for NIC interrupt and network softirq processing.

The experiment then measures:

Guest throughput / PPS
Guest CPU utilization
Guest netperf CPU utilization
Host vCPU utilization
Host physical-CPU placement

while preserving the same netperf message sizes and monitoring structure used in the previous container experiments.
