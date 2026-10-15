# Windows and Linux Fundamentals

Before moving on to SOC tools like Wazuh, I spent some time on the basic admin tasks for both Windows and Linux. On Windows, I already work in my AD lab, so this was about using the built-in tools more deliberately. On Linux, I started from scratch: I built an Ubuntu Server 26.04 LTS VM in VirtualBox with no GUI, so I had to do everything from the command line.

## What I practiced

**Windows**
- Task Manager and Resource Monitor (`resmon`) for checking processes and resource use
- Managing services in `services.msc`
- Creating and listing local users in Computer Management and PowerShell (`Get-LocalUser`, `New-LocalUser`)
- Basic PowerShell, including finding the top CPU users:
  ```powershell
  Get-Process | Sort-Object CPU -Descending | Select-Object -First 5
  ```

**Linux (Ubuntu Server)**
- Navigating and searching files: `pwd`, `ls -la`, `cd`, `mkdir`, `cp`, `mv`, `find`, `grep`
- Reading `rwx` permissions and changing them with `chmod` and `chown`
- Managing services with `systemctl` (stopping and restarting SSH)
- Installing packages with `apt` (installed `tree` to go through update, install, and use)
- Reading logs with `journalctl`: `sudo journalctl -n 20` for recent system activity, and `sudo journalctl -u ssh -n 20` to see what was logged when I restarted SSH

## What I learned

Windows and Linux show security activity in very different ways. Windows has Event Viewer with numbered Event IDs, and Linux has the systemd journal and `journalctl`. The question you're answering is the same on both: who did what, and when. Knowing that has been more useful to me than memorizing individual commands.

## Files

- [Progress journal](windows-linux-fundamentals-journal.md): what I worked through and what stood out
- [Cheat sheet](windows-linux-fundamentals-cheatsheet.md): commands and key Windows Event IDs for quick reference

I didn't take screenshots for this one. It's written notes only.
