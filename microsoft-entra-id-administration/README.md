# Microsoft Entra ID Administration

I set up my own Microsoft Entra tenant and worked through the identity tasks a help desk or junior admin handles most often: creating users and groups, resetting a password, assigning an admin role, onboarding a new hire, and offboarding someone who's leaving. I also reviewed the tenant's authentication settings and checked my changes in the audit logs.

Northstar Solutions and its employees are fictional, and so are the reasons behind each task (a forgotten password, a new hire, someone leaving). The accounts, groups, role assignment, and changes are real. I made them in my tenant through the Microsoft Entra admin center, and the screenshots show the results.

## Environment

- **Tenant:** my own Microsoft Entra tenant ("Default Directory"), managed through the Microsoft Entra admin center
- **Admin account:** my own account, which I used for every change
- **Test users:** five fictional Northstar Solutions employees, plus one more added during onboarding

The admin role in this lab, Helpdesk Administrator, is an **Entra directory role**: it controls what someone can do in the directory. Access to Azure resources is handled separately by Azure RBAC roles, which I covered in my [Azure RBAC & Storage Security Lab](../azure-rbac-storage-security-lab/).

## Lab notes

| # | Activity | What's in it |
|---|---|---|
| 01 | [User accounts](lab-notes/01-user-accounts.md) | Five Northstar employee accounts |
| 02 | [Security groups and membership](lab-notes/02-security-groups.md) | NS-IT, NS-HR, NS-Finance, NS-Sales and who's in them |
| 03 | [Password reset and audit verification](lab-notes/03-password-reset.md) | Sarah Johnson's reset, confirmed in the audit log |
| 04 | [Administrative role assignment](lab-notes/04-admin-role-assignment.md) | Helpdesk Administrator for John Smith, compared with Global Administrator |
| 05 | [Authentication methods and security defaults](lab-notes/05-authentication-methods-and-security-defaults.md) | Method policies, Authenticator settings, security defaults |
| 06 | [Employee onboarding](lab-notes/06-onboarding.md) | Olivia Martinez's account and NS-Finance membership |
| 07 | [Employee offboarding](lab-notes/07-offboarding.md) | Disabling Michael Brown, removing NS-Sales, revoking sessions |
| 08 | [Audit and sign-in log review](lab-notes/08-audit-log-review.md) | Matching audit entries to the work, and who actually signed in |

## Results

| Task | Verified by |
|---|---|
| 5 test users created | Users list |
| 4 security groups created | Groups list |
| Group memberships | NS-IT and NS-Finance member pages (NS-HR not captured) |
| Sarah Johnson's password reset | Audit log: Reset user password, success, target Sarah Johnson |
| John Smith assigned Helpdesk Administrator | Assigned roles: Direct, built-in, directory scope |
| Security defaults enabled | Tenant properties |
| Olivia Martinez onboarded | Audit log Add user entry, NS-Finance members |
| Michael Brown offboarded | Disabled status, 0 groups, NS-Sales empty, session revocation confirmed |

## Limitations

- I didn't sign in as any test user. That means the temporary password, John's admin role, MFA registration, and Michael's blocked access were all checked from the admin side only.
- I didn't configure or test Conditional Access, and I didn't trigger an MFA challenge.
- NS-HR's membership isn't captured in a screenshot.

## Evidence

Screenshots are in [evidence/](evidence/), and each lab note links to the ones it uses. I left out the password reset panel, because it shows the temporary password field, and the sign-in log detail, because it shows my personal email and session identifiers. In the published screenshots, I redacted the tenant ID, my email address, and the tenant domain (it contains my email address).
