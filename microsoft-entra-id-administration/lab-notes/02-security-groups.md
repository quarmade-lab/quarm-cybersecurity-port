# 02 — Security Groups and Membership

## Scenario

Northstar organizes access by department, so each department needed its own security group.

## What I did

Under **Groups → New group**, I created four security groups with assigned (manual) membership:

- **NS-IT**
- **NS-HR**
- **NS-Finance**
- **NS-Sales**

I then added employees to the groups and checked the **Members** page for each group I documented.

## What I observed

The All groups page listed four groups, each with group type Security and membership type Assigned.

| Group | Members |
|---|---|
| NS-IT | David Wilson, John Smith |
| NS-Finance | Sarah Johnson (plus Olivia Martinez after [onboarding](06-onboarding.md)) |
| NS-Sales | Michael Brown, until I removed him during [offboarding](07-offboarding.md). The published screenshot shows the group empty afterward. |
| NS-HR | Not captured |

I didn't screenshot NS-HR's members or Emily Davis's group membership, so I can't show those here.

## Result

All four groups existed, and NS-IT and NS-Finance have screenshots of their members. NS-Sales's membership shows up only through the offboarding change.

## Evidence

The four security groups (admin account name redacted):

![NS-Finance, NS-HR, NS-IT, NS-Sales security groups](../evidence/02-security-groups.png)

NS-IT members:

![NS-IT members](../evidence/03-ns-it-members.png)

NS-Finance members are shown in [06 — Onboarding](06-onboarding.md#evidence), and the empty NS-Sales group in [07 — Offboarding](07-offboarding.md#evidence).
