# Azure RBAC & Storage Security Lab

I used my own Azure subscription to practice resource-level access control. I created a resource group and storage account, gave a test user a role on the resource group, checked what that user could and couldn't do, and then cleaned everything up. Along the way I reviewed the storage account's security settings, the Activity Log, and the cost.

Northstar Solutions and its employee, Alex Morgan, are fictional. The resources, role assignments, errors, and log entries are real. They come from my subscription, and the screenshots show them.

This is a separate project from my [Microsoft Entra ID Administration](../microsoft-entra-id-administration/) lab. That project uses **Entra directory roles** (like Helpdesk Administrator), which control what someone can do in the directory. This one uses **Azure RBAC roles** (Owner and Contributor), which control what someone can do with Azure resources like resource groups and storage accounts. Alex's account lived in the same Entra tenant, but every role in this lab was an Azure resource role.

## Environment

- **Subscription:** Azure subscription 1 (free credit), managed in the Azure portal
- **Region:** Canada Central
- **Admin account:** my own, with Owner assigned at the subscription scope
- **Test user:** Alex Morgan, a member account I created in my Entra tenant for this lab
- **Resources:** resource group `rg-northstar-rbac-lab`, storage account `nsrbaclab1`, Blob container `northstar-documents`

## Lab notes

| # | Activity | What's in it |
|---|---|---|
| 01 | [Resource deployment](lab-notes/01-resource-deployment.md) | Resource group, storage account, and private container |
| 02 | [RBAC role assignment and tag tests](lab-notes/02-rbac-role-assignment.md) | Denied and allowed tag writes as Alex, Contributor at resource group scope, my inherited Owner role |
| 03 | [Blob container access test](lab-notes/03-storage-access-test.md) | The authorization error Alex got on the container, and management vs. data permissions |
| 04 | [Role removal](lab-notes/04-role-removal-and-verification.md) | Removing Contributor and confirming it in IAM |
| 05 | [Storage security review](lab-notes/05-storage-security-review.md) | Secure transfer, anonymous access, TLS, network access, key access |
| 06 | [Activity Log review](lab-notes/06-activity-log-review.md) | Role assignment, tag, and deployment events |
| 07 | [Cost monitoring and cleanup](lab-notes/07-cost-monitoring-and-cleanup.md) | Cost analysis, deleting Alex Morgan and the resource group |

## Results

| Check | Result |
|---|---|
| Resources deployed | `rg-northstar-rbac-lab` and `nsrbaclab1` (StorageV2, LRS, Canada Central), with private container `northstar-documents` |
| Tag write as Alex (about 4:10 AM, before the Contributor assignment) | Denied: AuthorizationFailed |
| Contributor for Alex at resource group scope | Assigned; IAM showed it on "This resource" and my Owner as "Subscription (Inherited)" |
| Tag write as Alex with Contributor | Succeeded, and logged in the Activity Log |
| Opening the Blob container as Alex | Authorization error on `Microsoft.Storage/storageAccounts/read` while the portal tried the access key |
| Contributor removed | Confirmed by portal notification and IAM list |
| Storage settings | HTTPS-only, TLS 1.2, anonymous access off; public network access and key access left on |
| Cost | Less than CA$0.01 accumulated when I checked |
| Cleanup | Alex Morgan deleted; resource group gone (404) |

## What I didn't test

- I didn't retest Alex's access after removing Contributor. I deleted the account instead.
- I didn't assign a Blob data role (like Storage Blob Data Reader), so I never tested reading blobs through Entra authorization.
- I can't show which role the earlier role assignment (about nine hours before my Activity Log review) granted.
- I don't know whether Contributor was still active when Alex got the container error. The timing is laid out in [note 03](lab-notes/03-storage-access-test.md#what-i-cant-explain-from-my-evidence).

## Evidence

Screenshots are in [evidence/](evidence/), and each lab note links to the ones it uses. In every published screenshot, I redacted subscription IDs, the tenant domain (it contains my personal email address), email addresses, object IDs, and a session ID.
