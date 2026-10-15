# KB-003 — Windows Printer and Print Spooler Troubleshooting

First-line checks for Windows printing problems: stuck jobs, an offline printer, or a Print Spooler service that keeps stopping.

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

## Escalation

Escalate recurring incidents, hardware failures, network printer connectivity problems, and driver issues that need elevated permissions.

## Example: NSIT-6

For [NSIT-6](../tickets/NSIT-6-printer-investigation.md), I ran steps 2 and 3 on my laptop. Print Spooler was running with startup type Automatic, and the print queue showed no jobs. That ruled out the spooler and a stuck queue on that machine, but it didn't reproduce the shared-printer problem. Steps 4 and 5 would have needed the actual printer.
