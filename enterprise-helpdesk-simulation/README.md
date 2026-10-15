# Enterprise IT Help Desk & ITIL Service Management Simulation

## Project Overview

This project simulates a Level 1 IT Service Desk supporting Northstar Solutions, a fictional organization with 50 employees.

The objective is to demonstrate practical IT support skills using Jira Service Management, including ticket intake, incident prioritization, troubleshooting, service requests, escalation, knowledge-base documentation, and ITIL-aligned service management.

**Environment:** Simulated enterprise IT support environment  
**Platform:** Jira Service Management Cloud  
**Role:** Simulated Tier 1 IT Support Technician  
**Project Key:** NSIT  
**Status:** Completed

## Business Scenario

Northstar Solutions requires a centralized IT support service to handle employee technical issues and requests.

Common support scenarios include:

- Windows login and password issues
- Network and DNS connectivity problems
- Printer troubleshooting
- Microsoft 365 authentication issues
- Software installation requests
- New employee onboarding
- Shared-folder access issues
- Workstation performance problems

## Project Objectives

1. Configure a functional IT service desk.
2. Organize incoming requests by category and priority.
3. Simulate realistic support tickets.
4. Investigate and document technical issues.
5. Apply ITIL incident and service request practices.
6. Document resolutions and escalation decisions.
7. Create reusable knowledge-base articles.
8. Capture evidence of the completed workflows.

## Tools and Technologies

- Jira Service Management
- Windows troubleshooting utilities
- Windows Event Viewer
- Active Directory lab (where applicable)
- Command Prompt and PowerShell
- GitHub
- ITIL 4 service management concepts

## Implementation Log

### Phase 1 — Service Desk Setup

**Status:** In progress

Planned activities:
- Create the Jira service project.
- Configure request types and categories.
- Review ticket queues and workflows.
- Establish sample prioritization and SLA targets.

#### Jira Service Desk — Initial Setup

Created the Northstar IT Service Desk using Jira Service Management's IT Service Management template.

![Northstar IT Service Desk Dashboard](evidence/01-jira-service-desk-created.png)

### Phase 2 — Incident and Request Simulation

**Status:** In progress

#### NSIT-1 — Windows Domain Login Investigation

Created and investigated a simulated Windows authentication incident using Jira Service Management and an existing Active Directory lab.

**Activities performed:**
- Registered and prioritized an incident in Jira.
- Investigated an Active Directory test account.
- Verified account status using PowerShell.
- Reviewed Windows Security Event ID 4625.
- Inspected failed-login records in Event Viewer.
- Performed an administrative password-reset exercise.
- Documented investigation findings and verification limitations.

**Verified findings:**
- Account enabled: True
- Account locked: False
- Password expired: False
- Five historical failed-logon events identified on DC01.

**Outcome:** The password-reset exercise was completed. Successful workstation sign-in was not independently verified, and the root cause was not conclusively established.

**Incident report:** [NSIT-1 — Windows Login Investigation](tickets/NSIT-1-windows-login.md)

**Supporting evidence:** [View screenshots](evidence/)

### Phase 3 — Troubleshooting and Resolution

Not started.

### Phase 4 — ITIL Documentation and Knowledge Base

Not started.

## Results

### Completed Work

- Deployed a simulated IT Service Desk using Jira Service Management.
- Created and documented the first incident, NSIT-1.
- Applied incident classification and prioritization.
- Used Active Directory and PowerShell to investigate account status.
- Reviewed Windows authentication logs.
- Performed an administrative password-reset exercise.
- Captured and organized supporting evidence in GitHub.

### Skills Demonstrated

- IT Service Management
- ITIL-aligned incident management
- Jira Service Management
- Active Directory administration
- Windows Server troubleshooting
- PowerShell
- Windows Event Viewer
- Technical documentation

### Current Limitations

The project uses a simulated business environment. The first incident demonstrated account investigation and password-reset procedures, but did not verify successful workstation sign-in or conclusively establish the original failure cause.

Additional service request, escalation, and knowledge-base workflows are planned.

## IT Support Ticket Portfolio

This project demonstrates hands-on familiarity with Jira Service Management, ITIL-aligned service desk workflows, Windows troubleshooting, and technical documentation.

The organization and employee scenarios are fictional. Technical findings are supported by controlled Windows lab exercises.

### Jira Service Desk Cases

| Ticket | Scenario | ITIL Practice | Report |
|---|---|---|---|
| NSIT-1 | Windows login investigation | Incident Management | [View](tickets/NSIT-1-windows-login.md) |
| NSIT-2 | New employee onboarding | Service Request Management | [View](tickets/NSIT-2-employee-onboarding.md) |
| NSIT-3 | Network and DNS troubleshooting | Incident Management | [View](tickets/NSIT-3-network-troubleshooting.md) |
| NSIT-4 | Windows performance investigation | Incident Management | [View](tickets/NSIT-4-windows-performance.md) |
| NSIT-5 | Software availability and verification | Service Request Management | [View](tickets/NSIT-5-software-installation.md) |
| NSIT-6 | Printer troubleshooting | Incident / Problem Management | [View](tickets/NSIT-6-printer-investigation.md) |

### Knowledge Base

- [KB-001 — Active Directory Password Reset](knowledge-base/KB-001-password-reset.md)
- [KB-002 — Network and DNS Troubleshooting](knowledge-base/KB-002-network-troubleshooting.md)
- [KB-003 — Windows Printer Troubleshooting](knowledge-base/KB-003-printer-troubleshooting.md)

### Jira Service Management Evidence

**Service Desk Queue**

![Jira service desk queue](evidence/17-jira-service-desk-queue.png)

**SLA Tracking**

![Jira SLA tracking](evidence/18-jira-sla-tracking.png)

### Skills Demonstrated

- Jira Service Management ticket creation, assignment, and tracking
- ITIL Incident Management
- ITIL Service Request Management
- Problem Management concepts
- Ticket prioritization and escalation
- SLA monitoring
- Active Directory account recovery procedures
- Windows desktop troubleshooting
- Network and DNS diagnostics
- Software inventory and functional testing
- Print Spooler and printer queue investigation
- Knowledge-base documentation
- GitHub technical reporting

### Scope and Limitations

This is an independent IT support simulation, not production service desk employment.

Technical exercises were performed in controlled lab environments. Fictional employee incidents remain open or pending where successful user-side resolution could not be verified.

## Disclaimer

This is an independent training project using fictional employees, simulated tickets, and controlled lab environments. It does not represent employment at Northstar Solutions or production IT support experience.
