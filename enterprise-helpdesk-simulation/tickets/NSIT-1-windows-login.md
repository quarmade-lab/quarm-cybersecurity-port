# NSIT-1 — Employee Can't Sign In to Windows

**Type:** Incident · **Priority:** Medium (single user, medium urgency) · **Jira status:** Pending

## The ticket

A fictional Finance employee, "John Smith", reported repeated failures signing in to his Windows workstation with his domain credentials. He wasn't sure if his password had expired or his account was locked.

I used the `testuser` account ("Test User") on my lab domain controller, `DC01.quarm.local`, to stand in for his account.

## What I did

**1. Found the account.** In Active Directory Users and Computers, I located Test User in the `Test Users` OU and checked its Account tab. "Password never expires" is turned on for this account.

**2. Checked account status in PowerShell.**

```powershell
Get-ADUser -Filter 'Name -eq "Test User"' -Properties Enabled,LockedOut,PasswordExpired,PasswordLastSet |
  Select-Object Name,SamAccountName,Enabled,LockedOut,PasswordExpired,PasswordLastSet
```

| Property | Result |
|---|---|
| Enabled | True |
| LockedOut | False |
| PasswordExpired | False |
| PasswordLastSet | 6/25/2026 7:07:12 PM |

So the account was enabled, not locked, and the password wasn't expired. That ruled out the two things the user was worried about.

**3. Looked for failed logons.** Event Viewer showed 18 Event ID 4625 entries in the Security log. I pulled the five most recent with:

```powershell
Get-WinEvent -FilterHashtable @{LogName='Security'; ID=4625} -MaxEvents 5 |
  Select-Object TimeCreated,Id,MachineName | Format-Table -AutoSize
```

What the evidence confirms:

- All five events were logged on DC01 on 9/16/2026, between 4:51:51 and 4:52:15 PM.
- I opened one of them (4:52:10 PM) in Event Viewer. It was for `testuser`, with status `0xC000006D` (unknown username or bad password). I didn't open the other four, so I haven't confirmed their account names.
- During my lockout-policy test in the [Windows Failed Login Investigation](../../windows-log-investigation/INC-001-failed-logon-investigation.md), Event ID 4740 recorded `testuser` being locked out at 4:52:15 PM on the same day.

What I'm inferring: the matching date, account, and end time point to these failures coming from my own `runas` lockout test, not from anything related to this ticket. I haven't matched each event to a specific attempt, though, so this is my best explanation rather than a confirmed one.

**4. Reset the password.** I right-clicked the account in ADUC, chose **Reset Password**, and got the confirmation "The password for Test User has been changed."

## Result

The password reset worked, but I can't call the incident resolved:

- I didn't test an interactive sign-in from a domain-joined workstation after the reset.
- The account showed no problems that would explain the reported failure, so the root cause is still unknown.

That's why the ticket is at **Pending** rather than Resolved. The next step would be to have the user try signing in with the new temporary password and note the exact error if it still fails.

## Screenshots

Incident logged in Jira:

![NSIT-1 in Jira](../evidence/02-first-incident-created.png)

Test User's Account tab in ADUC:

![Test User account properties](../evidence/03-ad-user-account-check.png)

`Get-ADUser` output:

![Account status in PowerShell](../evidence/04-ad-account-status.png)

The five most recent 4625 events from `Get-WinEvent`:

![Get-WinEvent output](../evidence/05-authentication-event-check.png)

One of those events open in Event Viewer (18 total in the filtered log):

![Failed logon event in Event Viewer](../evidence/06-failed-login-analysis.png)

Password reset confirmation:

![Password reset confirmation](../evidence/07-ad-password-reset-confirmation.png)

Related KB article: [KB-001 — Active Directory Password Reset](../knowledge-base/KB-001-password-reset.md)
