# NSIT-5 — Software Installation and Verification

## Project Overview

This exercise simulates a Level 1 IT support request for a PDF reader. The technician checks software inventory, confirms whether installation is required, and performs an application functionality test.

## Ticket Information

**Jira Ticket:** NSIT-5 (verify actual ticket ID)  
**Ticket Type:** Service Request  
**ITIL Practice:** Service Request Management  
**Environment:** Windows 11 workstation  
**Status:** In Progress

## Business Scenario

A fictional Finance employee requests a PDF reader to open and review business documents.

The technician must confirm whether an approved application is already available before attempting a new installation.

## Software Inventory Investigation

Navigated to:

**Windows Settings → Apps → Installed apps**

Searched for Adobe applications.

### Findings

| Attribute | Result |
|---|---|
| Application | Adobe Acrobat (64-bit) |
| Version | 26.002.21931 |
| Installation date | September 18, 2026 |
| Installed size | 1.14 GB |
| Installation required | No, application already present |

## Functional Verification

**Procedure:**
1. Launched Adobe Acrobat.
2. Opened a sample PDF document.
3. Verified that the document displayed successfully.

**Result:** Passed — Adobe Acrobat opened and displayed a PDF document without an observed error.

## Technical Assessment

Adobe Acrobat (64-bit), version 26.002.21931, was already installed on the tested Windows workstation.

The application launched successfully and displayed a PDF document. No new installation was required.

## Outcome

**Software inventory check:** Completed.  
**Functional verification:** Passed.  
**New installation performed:** No.  
**Lab exercise:** Completed.  
**Production request fulfilled:** Not verified; the fictional employee's workstation was not tested.

## Evidence

### Installed Software

![Adobe Acrobat installed](../evidence/13-nsit5-software-installed.png)

### Functional Test

![Adobe Acrobat displaying a PDF](../evidence/14-nsit5-pdf-functional-test.png)

## Skills Demonstrated

- Windows software inventory
- Application troubleshooting
- Software request assessment
- Functional verification
- ITIL Service Request Management
- Jira Service Management
- Technical documentation

---

*This exercise uses a fictional service request and actual software verification on a personal Windows workstation.*
