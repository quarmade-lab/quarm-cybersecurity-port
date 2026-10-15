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

## Disclaimer

This is an independent training project using fictional employees, simulated tickets, and controlled lab environments. It does not represent employment at Northstar Solutions or production IT support experience.
