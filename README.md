# livestats_view

**livestats_view** is a lean, real-time Linux system telemetry tool for engineers and performance professionals.  
It prints live, interval-based deltas for CPU, memory, network, and disk statistics directly to your terminal—no logging, no analysis, just the numbers you need as they happen.

- **Copyright (C) 2025 Laurence Oberman**
- *ChatGPT (OpenAI) assisted with design and implementation*
- **License:** GPL v3+

---

## Features

- **Live output:** No capture files, just deltas at your chosen interval
- **Covers the essentials:**  
  - **CPU:** User/system/idle/IOwait/Nice/Guest with running/blocked counts  
  - **Memory:** Used/Free/Available/Cached, in MB and %
  - **Network:** Per-interface RX/TX throughput, packets, errors, drops
  - **Disk:** Per-device Reads/Writes, throughput, queue length, awaits, plus totals
- **Device filtering:** Focus on a particular disk or class (e.g., `nvme`, `sda`)
- **No dependencies** beyond Rust and [chrono]

---

## Usage

```sh
livestats_view -g <interval_seconds> -pC           # CPU stats
livestats_view -g <interval_seconds> -pM           # Memory stats
livestats_view -g <interval_seconds> -pN           # Network stats
livestats_view -g <interval_seconds> -pD [-d DEV]  # Disk stats (optional filter)
Examples
sh
Copy code
livestats_view -g 1 -pC                # Show CPU every second
livestats_view -g 2 -pM                # Show memory every 2 seconds
livestats_view -g 1 -pN                # Show network stats live
livestats_view -g 1 -pD                # Show all disks/partitions
livestats_view -g 1 -pD -d nvme        # Only show disks with "nvme" in their name
Sample Output
CPU
scss
Copy code
Time     User(%)   Sys(%)   Idle(%)  IOWait(%)  Nice(%)  Running  Blocked  Guest(%)
15:13:20     0.05     0.10    99.55       0.10     0.00        1        0      0.00
Memory
scss
Copy code
Time      Used(MB)  Free(MB)    %Used   %Avail  %Cached   %Free  Cached(MB)
15:13:21     58124     5164     91.50     77.10    70.80    8.13      44883
Network
bash
Copy code
Time     Iface       rx_kB/s  tx_kB/s  rx_pkts  tx_pkts  rx_err  tx_err  drop
15:13:22 enp3s0         0.00     0.01        0        1       0       0     0
Disk
bash
Copy code
Time     Device     Reads/s  Writes/s  rd_kB/s  wr_kB/s  Qlen  await_rd(ms)  await_wr(ms)  total_kB/s  total_iops
15:13:23 nvme0n1    8043.00   5379.00  2065432.00 1373288.00 44.23  4.58    0.34  3438720.00 13422.00
Options
-g <interval_seconds>
Polling interval, in seconds (e.g., 1 = every second)

-pC
Show CPU stats

-pM
Show memory stats

-pN
Show network stats

-pD
Show disk stats (all block devices by default)

-d <substring>
(Optional, with -pD only) Filter to devices whose name contains this substring

Attribution
Primary author: Laurence Oberman (loberman@redhat.com)

AI co-author: ChatGPT (OpenAI), assisted with code, logic, and documentation

License: GPL v3+

Disclaimer
This tool is provided as-is, without warranty or support, for educational and diagnostic use in Linux environments.

Building
Standard Rust toolchain required:

sh
Copy code
cargo build --release
Feedback and contributions welcome!

yaml
Copy code

---

If you want any tweaks (shorter/longer, add more examples, different wording), just ask!  
You can copy-paste this as your `README.md` in your repo, and you’re ready to go.
