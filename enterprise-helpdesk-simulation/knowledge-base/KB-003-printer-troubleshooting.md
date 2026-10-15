# KB-003 — Windows Printer and Print Spooler Troubleshooting

## Purpose

Provide Level 1 IT support steps for investigating Windows printing failures, stuck jobs, and Print Spooler service issues.

## Common Symptoms

- Documents remain stuck in the print queue.
- Printer shows offline.
- Print jobs disappear without printing.
- Printer is unavailable to one or multiple users.
- Print Spooler service stops unexpectedly.

## Troubleshooting Procedure

### Step 1 — Identify the Affected Printer

Confirm:

- Printer name and location
- Connection type (USB, network, or shared)
- Number of affected users
- Error messages
- Whether the printer works from another device

### Step 2 — Inspect Print Spooler

1. Press **Windows + R**.
2. Enter `services.msc`.
3. Locate **Print Spooler**.
4. Open **Properties**.
5. Review **Service status** and **Startup type**.

Do not restart the service without considering its effect on active print jobs and other users.

### Step 3 — Inspect the Print Queue

1. Open **Settings → Bluetooth & devices → Printers & scanners**.
2. Select the affected printer.
3. Open its print queue.
4. Check for stuck, failed, or pending print jobs.

Do not delete other users' print jobs without authorization.

### Step 4 — Check Connectivity

For network printers, confirm that the workstation can communicate with the printer's configured network address.

For USB printers, check the cable and device connection.

### Step 5 — Review Driver and Configuration

Verify the installed printer driver, selected printer, and device status.

Driver changes or reinstallations should follow organizational change procedures.

### Step 6 — Verify and Close

After an authorized corrective action, print a test page and confirm the issue is resolved with the affected user.

Document the result before closing the incident.

## Lab Findings — NSIT-6

| Check | Observation |
|---|---|
| Print Spooler | Running |
| Startup type | Automatic |
| Print queue | No print jobs |
| Stuck jobs | None visible |
| Root cause | Not established |

The local diagnostic exercise did not reproduce the fictional shared-printer problem.

## Escalation

Escalate recurring incidents, hardware failures, network printer connectivity issues, and driver problems requiring elevated permissions.

## Related Lab

[NSIT-6 — Printer Investigation](../tickets/NSIT-6-printer-investigation.md)

---

*Prepared for a simulated IT support environment.*
