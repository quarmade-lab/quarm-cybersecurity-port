# Windows + Linux Fundamentals — Progress Journal

## What I was doing

I wanted to get solid on basic Windows and Linux administration before going deeper into SOC tools like Wazuh, which needs both.

## Windows side

I already spend a lot of time in Windows through my AD lab, so this was mostly about being deliberate — actually opening Task Manager and Resource Monitor and understanding what each tab is for, instead of just closing whatever's frozen. I went through `services.msc`, practiced managing local users both through the GUI (Computer Management) and PowerShell (`Get-LocalUser`, `New-LocalUser`), and ran a few basic PowerShell one-liners. One I'll actually keep using:

```powershell
Get-Process | Sort-Object CPU -Descending | Select-Object -First 5
```

Shows the top 5 processes eating CPU. Small thing, but genuinely useful.

## Linux side

This is the part I hadn't touched before. I built a fresh Ubuntu Server VM in VirtualBox — no GUI, on purpose, so I'd actually be forced to use the command line instead of clicking around. Ended up on Ubuntu 26.04 LTS.

Worked through it in parts:

- **Navigation and files** — `pwd`, `ls -la`, `cd`, `mkdir`, `cp`, `mv`, `find`, `grep`
- **Permissions** — reading the `rwx` string in `ls -la`, then `chmod` and `chown`
- **Services with `systemctl`** — I'd actually already used `systemctl status` on the SSH service earlier without thinking of it as "part of the lesson," so this one clicked fast
- **Package management with `apt`** — installed `tree` just to watch a real package go through update → install → verify → use
- **Logs** — the part that connected back to everything else I've done

## Logs on the Linux side

Most guides point you to `/var/log/auth.log` and `/var/log/syslog`, the Linux equivalent of checking Event Viewer for Event ID 4625. On my Ubuntu 26.04 VM I used `journalctl` instead, which reads the systemd journal directly:

- `sudo journalctl -n 20` — the latest 20 entries system-wide
- `sudo journalctl -u ssh -n 20` — the latest 20 entries for just the SSH service, which showed me exactly what was logged when I stopped and restarted SSH earlier in the session

Same idea as Event Viewer, just a different tool and a different format.

## The connection that mattered more than any single command

Windows and Linux expose security-relevant activity in completely different ways — Event Viewer with numbered Event IDs on one side, log files or `journalctl` on the other — but the underlying question is the same either way: **who did what, and when.** That's the actual transferable skill here, not memorizing 20 commands.

## What's next

The plan is to set up Wazuh and point it at this same Ubuntu VM. That's when the logs will show something worth investigating, instead of just my own routine commands.
