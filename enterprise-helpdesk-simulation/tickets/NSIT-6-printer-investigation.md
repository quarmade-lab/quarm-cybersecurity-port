# NSIT-6 — Recurring Printer Problems

**Type:** Incident · **Priority:** Medium · **Jira status:** Work in progress

## The ticket

Several fictional employees reported intermittent printing failures. Jobs sat in the queue or never reached the shared office printer. I checked the Windows printing components on my own Windows 11 laptop.

## What I checked

**Print Spooler service.** I opened `services.msc` and then Print Spooler's properties:

| Setting | Value |
|---|---|
| Service name | Spooler |
| Executable | `C:\WINDOWS\System32\spoolsv.exe` |
| Startup type | Automatic |
| Status | Running |

**Print queue.** I opened the Windows Print Queue window. It showed "No print jobs", so nothing was stuck or pending. The screenshot doesn't show which printer was selected, so I can't say which device's queue this was.

## Result

The spooler was running and set to start automatically, and the queue was empty. That rules out a stopped spooler or a backed-up queue on this machine at the time I checked. It doesn't rule out the causes that usually explain intermittent printing problems, like the network connection to the printer, the driver, or the printer itself. I couldn't test any of those without the actual printer.

Since several users reported the same problem more than once, this would also be worth a separate problem record if it kept happening. The root cause is unknown, and the ticket stays in **Work in progress**.

## Screenshots

Print Spooler properties:

![Print Spooler service properties](../evidence/15-nsit6-print-spooler.png)

Print Queue showing no jobs:

![Print Queue with no print jobs](../evidence/16-nsit6-printer-queue.png)

Related KB article: [KB-003 — Printer and Print Spooler Troubleshooting](../knowledge-base/KB-003-printer-troubleshooting.md)
