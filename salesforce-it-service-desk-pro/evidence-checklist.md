# Evidence Checklist

This file tracks which screenshots are in [evidence/](evidence/) and which ones are still missing. "Captured" means the screenshot is in the repository. "Partly" means a screenshot exists but doesn't show everything the item needs.

## Status by feature

| # | Feature | Status | Current file | Still needed |
|---|---|---|---|---|
| 1 | IT Service Desk Pro application | Partly | `01-app-home-page.png` (app name and tabs) | App Manager entry or app settings showing developer name, navigation style, and assigned profile |
| 2 | Support Ticket object and fields | Partly | `06-support-ticket-fields.png` | The **Support Ticket Name** field definition showing Auto Number and `TKT-{0000}` (cut off in the current screenshot) |
| 3 | IT Asset object and fields | Captured | `07-it-asset-fields.png` | Optional: Asset Type and Asset Status picklist values |
| 4 | Lookup relationships | Partly | `06-support-ticket-fields.png`, `07-it-asset-fields.png`, `03-tkt-0001-ticket-record.png` | A ticket with **Assigned Technician** filled in. AST-0001's **Related** tab showing TKT-0001 |
| 5 | Support Ticket page layout | Partly | `03-tkt-0001-ticket-record.png` (the result on a record) | Optional: the Page Layout Editor showing the four sections |
| 6 | Lightning record page | Partly | `08-lightning-record-page-builder.png` | The **Activation** settings showing how the page is assigned to IT Service Desk Pro |
| 7 | Escalate Ticket Quick Action | Partly | `10-escalate-ticket-action.png` (dialog before saving) | The ticket after saving, with Priority High and Escalation Reason filled in |
| 8 | Resolve Ticket Quick Action | Partly | `11-resolve-ticket-action.png` (dialog on an already-resolved ticket) | The dialog on an open ticket, and the ticket after saving with Status Resolved and the note filled in |
| 9 | Resolution Date Flow | Partly | `12-stamp-ticket-resolution-date-flow.png` (canvas only) | The **entry condition**. The **Assignment element** settings. A **ticket with Resolution Date filled in** after resolving |
| 10 | Network Priority Flow | Partly | `13-prioritize-network-tickets-flow.png` (canvas only) | The **entry condition**. The **Assignment element** settings. A **new Network ticket entered as Low that saved as High** |
| 11 | Sample ticket records | Captured | `02-support-tickets-list-view.png`, `03-tkt-0001-ticket-record.png`, `09-tkt-0002-record-with-quick-actions.png` | Optional: TKT-0005 linked to AST-0002 |
| 12 | Sample IT asset records | Captured | `04-it-assets-list-view.png`, `05-ast-0001-asset-record.png` | Optional: AST-0002 record |
| 13 | Ticket list views | Partly | `02-support-tickets-list-view.png`, `04-it-assets-list-view.png` (Recently Viewed) | A named custom list view, if one was created, with its columns and filter |
| 14 | Reports | Partly | `14-tickets-by-status-report.png` | **Tickets by Priority** and **Tickets by Category** reports |
| 15 | Dashboard | Captured | `15-it-service-desk-dashboard.png` | Retake after clicking **Refresh**, so the status chart matches the report |
| 16 | Lightning Home Page | Partly | `01-app-home-page.png` (dashboard card shows a link, no charts) | Home page with the dashboard charts visible, or the component settings if they still don't show |
| 17 | Update Ticket Quick Action | Missing | None | The Update Ticket dialog, and a ticket after using it |

## Screenshots to capture, in order

Running these in this order also completes the tests in [Testing and validation](docs/09-testing-and-validation.md). Save each one in `evidence-raw/` first, check it, then copy it into `evidence/` with the name below.

1. `16-support-ticket-name-auto-number.png`: **Setup → Object Manager → Support Ticket → Fields & Relationships → Support Ticket Name**. Data Type and Display Format must be visible.
2. `17-resolution-flow-entry-condition.png`: open **Stamp Ticket Resolution Date** in Flow Builder, click the start element, then **Edit**. Show the condition and the "only when a record is updated to meet the condition requirements" option.
3. `18-resolution-flow-assignment.png`: click the **Stamp Resolution Date** element. Show `$Record.Resolution_Date__c` Equals `$Flow.CurrentDateTime`.
4. `19-network-flow-entry-condition.png`: the same as step 2, for **Prioritize Network Tickets**.
5. `20-network-flow-assignment.png`: the **Set Network Priority** element, showing `$Record.Priority__c` Equals High.
6. `21-tkt-0001-resolution-date.png`: open TKT-0001 and expand **Resolution**. If Resolution Date has a value, this confirms the Flow.
7. `22-update-ticket-action.png`: on TKT-0003, click **Update Ticket** and set Assigned Technician to your user. Take the screenshot before saving.
8. `23-tkt-0003-technician-assigned.png`: TKT-0003 after saving, showing Assigned Technician.
9. `24-tkt-0003-resolve-dialog.png`: on TKT-0003 (open, not yet resolved), click **Resolve Ticket** and enter a resolution note. Take the screenshot before saving.
10. `25-tkt-0003-resolved-with-date.png`: TKT-0003 after saving, with the **Resolution** section expanded. Status Resolved, Resolution Note, and Resolution Date should be visible.
11. `26-tkt-0005-escalated.png`: on TKT-0005, use **Escalate Ticket**, enter a reason, and save. Expand **Escalation** and take the screenshot.
12. `27-network-ticket-entered-low.png`: **Support Tickets → New**, Category Network, Priority Low, before saving.
13. `28-network-ticket-saved-high.png`: the same ticket after saving, showing Priority High.
14. `29-ast-0001-related-tickets.png`: on AST-0001, set **Contact** to Daniel Carter, save, and open the **Related** tab.
15. `30-tickets-by-priority-report.png`: open **Reports → Tickets by Priority**.
16. `31-tickets-by-category-report.png`: open **Reports → Tickets by Category**.
17. `15-it-service-desk-dashboard.png` (replace): open the dashboard, click **Refresh**, and retake.
18. `01-app-home-page.png` (replace if the charts appear): open the **Home** tab and let it finish loading.
19. `32-record-page-activation.png`: **Lightning App Builder → IT Support Ticket Record Page → Activation**.
20. `33-app-manager-settings.png`: **Setup → App Manager → IT Service Desk Pro → Edit**, App Details and User Profiles.

Optional: `34-page-layout-editor.png` (the four sections in the Page Layout Editor) and `35-tickets-custom-list-view.png` (a named list view, if you made one).

If a test fails, keep the screenshot anyway and name it for what it shows, for example `25-tkt-0003-resolution-date-empty.png`. A failed result is still evidence, and the docs should say what happened.

## Before adding any screenshot

- [ ] No browser address bar or org URL (`*.my.salesforce.com` or `*.lightning.force.com`)
- [ ] No record IDs in a URL
- [ ] No real email addresses. The fictional `daniel.carter@example.com` is fine, but a personal or work email isn't
- [ ] No usernames that are email addresses (Trailhead Playground usernames often are). Crop or blur them
- [ ] No session IDs, tokens, or Setup pages showing login history or security settings
- [ ] Only fictional sample data
- [ ] Descriptive filename that matches this list
- [ ] Linked from the right document, with a caption saying what it shows

After adding screenshots, update the matching document and the status tables in the [README](README.md#testing-and-current-status) and [Testing and validation](docs/09-testing-and-validation.md). Change "Not verified" to "Passed" only when the screenshot shows the result.
