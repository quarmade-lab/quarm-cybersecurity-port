# 10 — Troubleshooting and Lessons

These are the problems I ran into during the build, and what I did about each one. Not everything worked the first time.

## Problems during the build

### Fields stayed outside the new layout sections

- **Symptom:** I added Ticket Information, Assignment Details, Escalation, and Resolution sections to the page layout, but the fields didn't move into them.
- **Cause:** Adding a section only creates an empty container. Existing fields stay where they are.
- **Fix:** I dragged each field into its section in the Page Layout Editor and saved.

### Required fields missing from the layout

- **Symptom:** Salesforce warned that the required fields **Subject** and **Status** were missing from the page layout.
- **Cause:** I'd moved them out while rearranging sections.
- **Fix:** I put both back in Ticket Information and saved.
- **Lesson:** Required fields have to stay on any layout people use to create or edit records. Otherwise they can't fill them in, and the record can't be saved.

### Page layouts vs. Lightning record pages

- **Symptom:** I assumed page layouts and Lightning record pages were basically the same thing, and wasn't sure which tool to use for what.
- **Cause:** They're different tools. The page layout controls fields, sections, and some actions. Lightning App Builder controls the page structure and components.
- **Fix:** I used the page layout for field sections and Lightning App Builder for the Highlights Panel, Record Detail, related lists, and the guide panel. See [05](05-page-layouts-and-lightning-pages.md).

### "No data available" in the Lightning App Builder preview

- **Symptom:** Components showed "No data available" while I was building the record page.
- **Cause:** The preview had no record selected, so there was nothing to display.
- **Fix:** Nothing was broken. With a record to preview, or on a real ticket, the fields show their values.

### Lists only showed record names

- **Symptom:** The Support Tickets and IT Assets lists only showed TKT-0001 or AST-0001, so I had to open each record to see what it was.
- **Cause:** Salesforce controls list and search columns separately from the record page.
- **Fix:** I updated the objects' search layouts and list view columns. The ticket list now shows Subject, Priority, Category, and Assigned Technician. The asset list shows Asset Name, Asset Type, Asset Status, and Manufacturer.

### Dashboard component wouldn't load on the home page

- **Symptom:** Lightning App Builder showed **Invalid Component** for the Dashboard component, and searching for the dashboard returned no matches.
- **What I checked:** whether the dashboard was saved, its folder, whether I had access to it, and whether it appeared in the component's settings.
- **Result:** The error is gone in my final screenshot, and the component shows the dashboard's title and a View Dashboard link. The charts don't appear in the card, so this is only partly resolved. I didn't record which check fixed the error. See [08](08-reports-and-dashboard.md#the-dashboard-component-problem).

## Things the screenshots showed

These came up while I matched my screenshots to my notes.

| Finding | Why it matters | What I'd do |
|---|---|---|
| The ticket name field is labelled **Support Ticket Name**, not Ticket Number | The list and report columns say "Support Ticket Name" | Rename the label to Ticket Number. The values stay the same |
| The resolution field is **Resolution Note**, not Resolution Notes | Small, but my notes and the org disagree | Keep it, and use the real label in the docs (done) |
| The asset's employee lookup is labelled **Contact** | "Contact" doesn't say this is who the device is assigned to | Rename the label to Assigned To |
| **Description** sits above the sections, not in Ticket Information | It's separated from the rest of the ticket details | Move it into Ticket Information on the layout |
| Quick Action dialogs include **Subject, Priority, and Status** | Escalate shows a Status field, and Resolve shows Priority | Check whether the required fields can come off the action layouts |
| The dashboard data is older than the report | The status chart says 2 New, the report says 0 | Refresh the dashboard before taking screenshots |
| The Resolution Date Flow only runs on update | A ticket created as Resolved never gets a date | Change the trigger to "created or updated" |
| The Network Flow sets High even on Critical tickets | It could lower an urgent ticket | Add "Priority is not Critical" to the entry condition |

## What I learned

- **How the pieces connect.** The objects, fields, and lookups are what every page, action, Flow, and report builds on. Picklists made reporting and Flow conditions simple, because the values are always spelled the same way.
- **Lookups vs. master-detail.** Lookups fit records that live on their own, like people, devices, and tickets. Master-detail is for child records that shouldn't exist without the parent.
- **Layouts affect data entry, not just appearance.** Required fields have to stay where people can reach them.
- **Two tools shape a record page.** The page layout sets fields and sections. Lightning App Builder sets structure and components.
- **Lists are configured separately.** Search layouts and list views decide what shows up in lists and search results.
- **Before-save Flows are simple for same-record updates.** One Assignment element on `$Record` does it, without an Update Records element.
- **Record-triggered Flows can update data based on conditions.** Even a basic rule like "Network means High" showed me how the trigger, the entry condition, and the Assignment work together.
