# Lab Overview

## Purpose

The goal was practice with the server side of IT support: building a Windows Server, reaching it remotely, and doing the routine checks and fixes a junior admin is usually asked to do. Azure made that possible on a real Windows Server 2025 install without extra hardware, and everything could be deleted afterward.

This was a hands-on lab in my own Azure subscription. There were no real users, printers, or business services on the server.

## Scope

**In scope**

- Deploying one Windows Server 2025 VM in Azure
- Connecting over RDP with the local administrator account
- OS verification, local user creation, Windows updates, and service management with PowerShell
- Installing the Web Server (IIS) role
- A simulated Print Spooler outage, restored and verified
- Monitoring with Task Manager, Resource Monitor, Event Viewer, and Azure Monitor metrics
- Deleting all resources afterward

**Out of scope**

- Active Directory or domain join. This was a standalone server.
- Testing IIS by serving a web page
- Backups, alerting, or anything meant to keep the server running long term

## Environment

| Item | Value |
|---|---|
| Subscription | My own Azure subscription |
| Region | Canada Central |
| Resource group | `RG-ServerLab` |
| VM | `Quarm-Server01`, Standard D2als v7 (2 vCPUs, 4 GiB memory), Gen 2, x64 |
| OS | Windows Server 2025 Datacenter: Azure Edition, build 26100 |
| Networking | Public IP `Quarm-Server01-ip`, NSG `Quarm-Server01-nsg`, NIC `quarm-server01909`, virtual network `vnet-canadacentral-1` |
| Lab date | October 31, 2026 |

## How the docs are organized

1. [Deployment](deployment.md): creating the VM and connecting
2. [Administration](administration.md): PowerShell admin tasks
3. [Troubleshooting](troubleshooting.md): the Print Spooler outage
4. [Monitoring](monitoring.md): performance and log review
5. [Lessons learned](lessons-learned.md)
