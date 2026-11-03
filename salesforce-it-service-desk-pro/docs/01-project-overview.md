# 01 — Project Overview

## Goal

Build a working IT help desk application in Salesforce on my own, using what I'd learned on Trailhead about custom objects, relationships, Lightning App Builder, and Flow.

I'd done several guided Trailhead exercises and wanted to build my own application instead of following another one. I picked an IT help desk because IT support and systems administration are the areas I'm most interested in, and I wanted to build something close to what a real support team might use.

## The scenario

Employees at a fictional company run into everyday technical problems:

- Someone can't connect to the company VPN.
- A laptop won't turn on.
- Microsoft Teams stops working.
- Someone needs a password reset.
- An office printer stops responding.

Without a shared system, these requests get scattered across emails, messages, and conversations. Nobody can easily see what's open, who's working on it, or how it was fixed last time.

The app gives support staff one place to record the problem, link it to the employee and the device involved, assign a technician, track progress, escalate when needed, and record the fix.

## Scope

| In scope | Out of scope |
|---|---|
| Two custom objects, their fields, and four lookup relationships | Apex code, Lightning Web Components, or anything else that needs code |
| A Lightning app, page layout, Lightning record page, and home page | Separate profiles or permission sets for technicians and employees |
| Three Quick Actions for common ticket changes | Email notifications, assignment rules, or SLAs |
| Two record-triggered Flows | Screen Flows or an employee self-service form |
| Three reports and a dashboard | Exporting the configuration as metadata |
| Six sample tickets and two sample assets | Real users or real data |

The out-of-scope items are listed in the [README's future improvements](../README.md#future-improvements). None of them are built.

## Environment

| Item | Details |
|---|---|
| Platform | Salesforce Lightning Experience |
| Org | Salesforce Trailhead Playground (labelled Developer Edition in the org) |
| Approach | Point-and-click configuration only |
| Tools | App Manager, Object Manager, Lightning App Builder, Flow Builder, Reports, Dashboards |
| Intended users | IT technicians, support teams, and IT managers |
| My role | Org administrator, also acting as the technician |

## Timeline

These dates come from the screenshots:

| Date | What the screenshots show |
|---|---|
| 2026-11-01 | Both Flows last saved and active (version 1) |
| 2026-11-02 | TKT-0001 created at 6:26 p.m., TKT-0002 at 6:27 p.m., and AST-0001 at 6:30 p.m. The other records' creation times aren't captured |
| 2026-11-03 | Dashboard data as of 10:37 a.m., and the report, Quick Action, and list screenshots taken later that day |

## Where things stand

Most of the build is confirmed in screenshots: the app, both objects and their fields, the lookups, the record page, the Quick Action buttons, both active Flows, a report, and the dashboard.

The parts still to verify are:

- whether either Flow actually changed a record
- the saved results of the Quick Actions
- the data type of the Support Ticket name field
- whether the dashboard charts appear on the home page

[Testing and validation](09-testing-and-validation.md) has the full list and the steps to finish them.
