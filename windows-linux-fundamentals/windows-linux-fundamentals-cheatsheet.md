# Windows + Linux Fundamentals Cheat Sheet

Quick reference from working through — diagnostics, services, users, and logs on Windows and Ubuntu.

---

## Windows

### Diagnostics
- **Task Manager** (`Ctrl+Shift+Esc`) — Processes, Performance, Users, Startup tabs. First thing to open for "my computer is slow."
- **Resource Monitor** (`resmon`) — deeper than Task Manager; shows which specific process is holding a file, port, or handle.

### Services
- `services.msc` — GUI service management. Right-click a service for Start/Stop/Restart; Properties tab sets startup type (Automatic/Manual/Disabled).

### User Management
- GUI: `compmgmt.msc` → System Tools → Local Users and Groups
- PowerShell:
  ```
  Get-LocalUser
  New-LocalUser -Name "labtest" -Password (Read-Host -AsSecureString)
  ```

### PowerShell Basics
```powershell
$x = 5                                  # variable
1..5 | ForEach-Object { Write-Host $_ } # loop
Get-Process | Sort-Object CPU -Descending | Select-Object -First 5   # top 5 CPU-hungry processes
```

### Security / Event Logs
- Event Viewer → Windows Logs → **Security**
- Key Event IDs worth knowing on sight:
  - `4624` — successful logon
  - `4625` — failed logon
  - `4740` — account lockout
  - `4688` — process creation
  - `4720` — account created
  - `4728` / `4732` — added to a privileged/security group
  - `4698` — scheduled task created

---

## Linux (Ubuntu)

### Navigation & Files
```bash
pwd                     # where am I
ls -la                  # list everything, including hidden files, with detail
cd /path                # move
mkdir folder            # create a directory
cp source dest          # copy
mv source dest          # move/rename
find / -name "*.log" -type f 2>/dev/null   # search the whole system for files
grep -i 'keyword' file  # search inside a file's contents
```

### Permissions
- `ls -la` shows a string like `drwxr-xr-x` — type, then owner/group/other read-write-execute.
- `chmod 750 folder` — set permissions (owner: rwx, group: r-x, other: none)
- `chown user:group file` — change ownership

### Services
```bash
systemctl status <service>
sudo systemctl stop <service>
sudo systemctl start <service>
sudo systemctl enable <service>   # start automatically on boot
```

### Package Management
```bash
sudo apt update            # refresh the list of available packages (doesn't install anything)
sudo apt install -y <pkg>  # install a package
```

### Logs
- **Older Ubuntu / traditional setups:** `/var/log/auth.log` (authentication events), `/var/log/syslog` (general system activity)
- **Newer Ubuntu (26.04+ in my case):** these plain-text files may not exist at all — logging relies on `journald` instead. This isn't broken, it's just how modern systemd-based distros work.
  ```bash
  sudo journalctl -n 20          # latest 20 entries, system-wide
  sudo journalctl -u ssh -n 20   # latest 20 entries for one specific service
  ```

---

## Windows ↔ Linux Equivalents

| Task | Windows | Linux |
|---|---|---|
| Process/resource monitor | Task Manager / Resource Monitor | `top` / `htop` |
| Service management | `services.msc` | `systemctl` |
| Security & auth logs | Event Viewer (Security log, Event IDs) | `journalctl` / `/var/log/auth.log` |
| Local user management | `compmgmt.msc` / PowerShell | `/etc/passwd`, `useradd`, `usermod` |
| Software installation | Windows Update / manual installers | `apt` |
