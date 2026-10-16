# Quarm Adeniran — IT Support and Cybersecurity Portfolio

I'm a Computer Science graduate building hands-on labs to get practical with IT support, Windows administration, and security work. This repository is where I document what I set up, what I tested, and what I found, including the things that didn't fully work or that I couldn't verify.

Most of my lab work runs on a Windows Server 2022 domain controller (`DC01`, domain `quarm.local`) in VirtualBox, plus an Ubuntu Server VM, my own Windows 11 laptop, a Microsoft Entra test tenant, and an Azure subscription.

## What I'm working on

- Active Directory user, group, and permission management
- Microsoft Entra ID users, groups, admin roles, and authentication settings
- Azure RBAC role assignments and storage account security settings
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

### [Microsoft Entra ID Administration](microsoft-entra-id-administration/)
In my own Entra tenant, I created five test users and four security groups for a fictional company. I reset a password and confirmed it in the audit logs, and assigned the Helpdesk Administrator role as a direct assignment. I also onboarded a new hire, and offboarded a departing user by disabling the account, removing group membership, and revoking sessions. Along the way I reviewed authentication method policies and confirmed security defaults were on. All of this was checked from the admin side; I didn't sign in as the test users or test Conditional Access.

### [Azure RBAC & Storage Security Lab](azure-rbac-storage-security-lab/)
A separate lab on Azure resource access, as opposed to Entra directory roles. I deployed a resource group, storage account, and private Blob container, then gave a test user the Contributor role on the resource group. With that role, the user could write tags on the resource group, where an earlier attempt had been denied. When the user opened the Blob container, the portal showed an authorization error, which I used to work through how Azure management permissions differ from Blob data permissions. I also reviewed the storage account's security settings, the Activity Log, and the cost (under CA$0.01), then removed the role, deleted the user, and deleted the resource group.

### [Windows and Linux Fundamentals](windows-linux-fundamentals/)
Notes from practicing core admin tasks on Windows and on a command-line-only Ubuntu Server VM: services, users, permissions, packages, and logs, plus a quick-reference cheat sheet.

<!--### [Vulnerability Scanning Lab](vulnerability-scanning-lab/) — planned
Not started yet. The plan is to scan an intentionally vulnerable target in an isolated lab and write up the findings.-->

## Contact

- LinkedIn: https://www.linkedin.com/in/quarm-adeniran-8b6895419/
- Email: quarm1608@gmail.com
