# 09 — Testing and Validation

I planned these test cases while building the app. This page records which ones the screenshots confirm, which are partly confirmed, and which still need a test. Planning a test isn't the same as passing it, so the status column only says Passed when a screenshot shows the result.

## Results

| # | Test | Expected result | Status | Evidence or gap |
|---|---|---|---|---|
| 1 | Create a Support Ticket | Ticket saves with a generated name | **Passed** | Six tickets, TKT-0001 to TKT-0006 ([list](../evidence/02-support-tickets-list-view.png)) |
| 2 | Ticket name format | Names follow `TKT-{0000}` | **Partly** | Names follow the format and aren't editable. The field's data type isn't captured |
| 3 | Create an IT Asset | Asset saves as `AST-{0000}` | **Passed** | AST-0001 and AST-0002. Asset Number is Auto Number ([fields](../evidence/07-it-asset-fields.png)) |
| 4 | Link a reporter | Reported By links to a Contact | **Passed** | TKT-0001 → Daniel Carter ([record](../evidence/03-tkt-0001-ticket-record.png)) |
| 5 | Link an IT Asset | Ticket references the device | **Passed** | TKT-0001 → AST-0001, Dell Latitude 5440 |
| 6 | Assign a technician | Assigned Technician saves a User | **Not tested** | Empty on every ticket |
| 7 | Assign an asset to an employee | IT Asset Contact saves a Contact | **Not tested** | Empty on AST-0001 |
| 8 | Escalate Ticket | Priority and escalation reason update | **Partly** | Dialog opens with Priority = High on a Medium ticket. Not saved ([dialog](../evidence/10-escalate-ticket-action.png)) |
| 9 | Resolve Ticket | Status becomes Resolved and note is saved | **Partly** | Dialog opens with Resolution Note and Status = Resolved, but on a ticket that was already Resolved. Not saved |
| 10 | Update Ticket | Status, priority, technician, category update | **Not tested** | Button is on the page. No dialog or result captured |
| 11 | Resolution Date Flow | Resolution Date fills in when status changes to Resolved | **Not verified** | Flow is active. No screenshot shows a Resolution Date value |
| 12 | Network Priority Flow | New Network ticket saves as High | **Not verified** | Flow is active. Network tickets are High, but the entered priority wasn't recorded |
| 13 | Ticket reports | Ticket data appears in reports | **Passed** | Tickets by Status shows all six tickets ([report](../evidence/14-tickets-by-status-report.png)) |
| 14 | Dashboard | Charts reflect report data | **Passed, with a caveat** | Three charts render. Status chart data is from before two tickets were resolved ([dashboard](../evidence/15-it-service-desk-dashboard.png)) |
| 15 | Home page | Welcome text and dashboard charts on Home | **Partly** | Welcome text shows. Dashboard card shows a link but no charts ([home](../evidence/01-app-home-page.png)) |
| 16 | Lightning record page | Custom page shows on ticket records | **Passed** | Tickets in the app use IT Support Ticket Record Page |
| 17 | List columns | Lists show useful fields, not just names | **Passed** | Ticket and asset lists show subject, priority, category, and similar columns |

Score so far: 8 passed (one with a caveat), 4 partly, and 5 not tested or not verified.

## Remaining tests, step by step

Each of these ends with a screenshot. The [evidence checklist](../evidence-checklist.md) lists the filenames to use.

### Ticket name field (test 2)

1. Go to **Setup → Object Manager → Support Ticket → Fields & Relationships**.
2. Scroll to **Support Ticket Name** and click it.
3. Check that Data Type is **Auto Number** and Display Format is **TKT-{0000}**. Take a screenshot.

### Assign a technician (test 6) and Update Ticket (test 10)

1. Open TKT-0003 (Microsoft Teams won't open).
2. Click **Update Ticket**. Take a screenshot of the dialog.
3. Set **Assigned Technician** to your user and save.
4. The ticket should show your name under Assigned Technician. Take a screenshot.

### Escalate Ticket (test 8)

1. Open TKT-0005 (Office printer offline, Priority Low).
2. Click **Escalate Ticket**. Priority should already be High.
3. Enter an escalation reason, for example `Printer is shared by the whole floor and several people can't print.`, and save.
4. Expand **Escalation**. Priority should be High, and the reason should be saved. Take a screenshot.

### Resolve Ticket (test 9) and Resolution Date Flow (test 11)

1. First, open TKT-0001 and expand **Resolution**. If Resolution Date already has a value, take a screenshot. That alone confirms the Flow ran.
2. Open TKT-0003. Expand **Resolution** and confirm Resolution Date is empty.
3. Click **Resolve Ticket**, enter a resolution note, and save.
4. Status should be Resolved. Resolution Note and Resolution Date should both be filled in. Take a screenshot with the Resolution section expanded.

### Network Priority Flow (test 12)

1. Go to **Support Tickets → New**. Enter Subject `Wi-Fi drops in meeting room`, Category **Network**, and Priority **Low**. Take a screenshot before saving.
2. Save. Priority should be **High**. Take a screenshot.

### Assign an asset (test 7)

1. Open AST-0001. Set **Contact** to Daniel Carter and save.
2. Take a screenshot. Then open the **Related** tab and check whether TKT-0001 appears as a related Support Ticket. Take a screenshot of that too.

### Dashboard and home page (tests 14 and 15)

1. Open **Dashboards → IT Service Desk Dashboard** and click **Refresh**. The status chart should now match the report. Take a screenshot.
2. Open the app's **Home** tab and wait for it to load. Take a screenshot of whether the charts appear in the dashboard card.

## What isn't covered at all

- **Other users.** Every test was run as me, the System Administrator. I didn't test what a technician with fewer permissions could see or do.
- **Negative tests.** I didn't try saving a ticket without a Subject, or a Network ticket set to Critical (the Flow would lower it to High; see [07](07-flow-automation.md#why-this-rule-is-simple)).
- **Bulk changes.** I didn't import or bulk-update tickets to see how the Flows behave with many records at once.
