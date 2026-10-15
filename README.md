# Quarm Adeniran — IT Support and Cybersecurity Portfolio

I'm a Computer Science graduate building hands-on labs to get practical with IT support, Windows administration, and security work. This repository is where I document what I set up, what I tested, and what I found, including the things that didn't fully work or that I couldn't verify.

Most of my lab work runs on a Windows Server 2022 domain controller (`DC01`, domain `quarm.local`) in VirtualBox, plus an Ubuntu Server VM and my own Windows 11 laptop.

## What I'm working on

- Active Directory user, group, and permission management
- Help desk ticket handling in Jira Service Management
- Windows troubleshooting (networking, performance, services, printing)
- Windows Security log investigation and account lockout policy
- Linux command-line basics and `journalctl`

## Projects

### [Enterprise Help Desk Simulation](enterprise-helpdesk-simulation/)
I set up a Jira Service Management desk for a fictional 50-person company and worked six tickets (NSIT-1 to NSIT-6). The company and users are made up, but the technical checks were real: I checked an AD account's status with PowerShell and reset its password, pulled Event ID 4625 logs, ran `ipconfig`, `ping`, `nslookup`, and `tracert`, reviewed Task Manager performance data, verified an installed application, and inspected the Print Spooler service. I also wrote three knowledge-base articles. All six tickets are still open in Jira, because I couldn't confirm the fictional users' issues were fixed.

### [Windows Failed Login Investigation](windows-log-investigation/)
I generated failed logons on my domain controller with `runas`, then traced each Event ID 4625 in Event Viewer and decoded its status codes. I noticed that repeated bad passwords never locked the account, so I set up an account lockout policy. I worked through a GPO precedence problem with `gpresult` and confirmed the lockout with Event ID 4740.

### [Active Directory Help Desk Lab](active-directory-help-desk-lab/)
Four common help desk tasks on my domain controller: a password reset, disabling and re-enabling an account, adding a user to a VPN access group, and setting share and NTFS permissions on a Finance shared folder.

### [Windows and Linux Fundamentals](windows-linux-fundamentals/)
Notes from practicing core admin tasks on Windows and on a command-line-only Ubuntu Server VM: services, users, permissions, packages, and logs, plus a quick-reference cheat sheet.

<!--### [Vulnerability Scanning Lab](vulnerability-scanning-lab/) — planned
Not started yet. The plan is to scan an intentionally vulnerable target in an isolated lab and write up the findings.-->

## Contact

- LinkedIn: https://www.linkedin.com/in/quarm-adeniran-8b6895419/
- Email: quarm1608@gmail.com
