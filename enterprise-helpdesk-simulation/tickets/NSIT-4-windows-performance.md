# NSIT-4 — Slow Workstation

**Type:** Incident · **Priority:** Medium · **Jira status:** Work in progress

## The ticket

A fictional Administration employee reported slow app launches and a laptop that felt sluggish during normal work. I ran the checks on my own Windows 11 laptop, using Task Manager.

## What I found

**Performance tab**

| Resource | Reading |
|---|---|
| CPU (Intel Core Ultra 7 155H) | 2% utilization at 1.66 GHz |
| Memory | 12.0 GB of 15.4 GB in use (78%) |
| Disk 0 (C:, NVMe SSD) | 2% active time |
| Processes | 320 |
| Uptime | 3 days, 5 hours |

**Processes tab** — the biggest memory users:

| Process | Memory |
|---|---|
| Microsoft Edge (17 processes) | 1,527.1 MB |
| Claude (10 processes) | 436.0 MB |
| Photos (2 processes) | 308.1 MB |

## Result

CPU and disk were close to idle, so neither was a bottleneck when I looked. Memory was the only thing worth flagging: 78% in use, with Edge alone using about 1.5 GB. That isn't a problem by itself. But if the user opened a few more heavy apps, the system could start paging to disk and feel slow.

The catch is that I took one snapshot while the laptop was running fine. To actually diagnose slowness, I'd need to watch Task Manager or Resource Monitor while the slowdown is happening. I'd also probably start with a restart after three days of uptime and look at trimming browser tabs or startup apps. I didn't make any of those changes, so the root cause is unconfirmed and the ticket stays in **Work in progress**.

## Screenshots

Performance overview:

![Task Manager performance tab](../evidence/11-nsit4-performance-overview.png)

Running processes:

![Task Manager processes tab](../evidence/12-nsit4-running-processes.png)
