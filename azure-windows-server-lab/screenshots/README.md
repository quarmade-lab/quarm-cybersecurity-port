# Screenshots

All screenshots were taken during the lab on October 31, 2026. Redacted areas are covered with dark grey boxes.

| File | What it shows | Redacted |
|---|---|---|
| [vm-deployment.png](vm-deployment.png) | VM deployment in progress: NSG and public IP created | Correlation ID |
| [vm-overview.png](vm-overview.png) | `Quarm-Server01` overview: Running, Canada Central, Standard D2als v7 | Subscription ID, public IP (2 places) |
| [rdp-session.png](rdp-session.png) | Server Manager open in the RDP session | Public IP in the RDP bar |
| [powershell-system-info.png](powershell-system-info.png) | `hostname` and `Get-ComputerInfo`: Windows Server 2025 Datacenter Azure Edition, build 26100 | Public IP in the RDP bar |
| [local-user.png](local-user.png) | Creating `LabSupport` with `New-LocalUser` and listing accounts with `Get-LocalUser` | None (password was masked at entry) |
| [windows-update.png](windows-update.png) | Installed hotfixes from `Get-HotFix` | None |
| [service-troubleshooting.png](service-troubleshooting.png) | Print Spooler: Running, restarted, stopped, started, Running | Public IP in the RDP bar |
| [iis-install.png](iis-install.png) | Web Server (IIS) role installed and confirmed | Public IP in the RDP bar |
| [resource-monitor.png](resource-monitor.png) | Task Manager and Resource Monitor overview | Public IP in the RDP bar |
| [event-viewer.png](event-viewer.png) | System log with Service Control Manager Event ID 7036 entries | Public IP in the RDP bar |
| [azure-metrics.png](azure-metrics.png) | Avg Percentage CPU for the VM in Azure Monitor metrics | None |
| [resource-group.png](resource-group.png) | `RG-ServerLab` and its six resources, right before deletion | Subscription ID, email address, tenant domain |

`powershell-system-info.png` and `local-user.png` are two crops of the same PowerShell screenshot.
