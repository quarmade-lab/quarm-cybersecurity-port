# KB-001 — Windows Active Directory Password Reset

How to check why a user can't sign in to a domain account, and how to reset the password safely. Uses Active Directory Users and Computers (ADUC) and Event Viewer on the domain controller.

## Common Symptoms

- Employee cannot sign in to their Windows workstation.
- Incorrect username or password message.
- Account locked or disabled.
- Password expired.
- Domain authentication unavailable.

## Troubleshooting Procedure

### Step 1 — Verify the User

Confirm the employee's identity using the organization's approved verification procedure before making account changes.

Never request the employee's existing password.

### Step 2 — Locate the Account

1. Sign in to an authorized administrative workstation.
2. Open **Server Manager → Tools → Active Directory Users and Computers**.
3. Locate the appropriate organizational unit.
4. Find the affected employee's account.
5. Open **Properties** to review account details.

### Step 3 — Check Account Status

Verify whether the account is:

- Enabled or disabled
- Locked or unlocked
- Subject to password expiration
- Affected by account restrictions

PowerShell gives a quick summary:

```powershell
Get-ADUser -Identity <username> -Properties Enabled,LockedOut,PasswordExpired,PasswordLastSet |
  Select-Object Name,Enabled,LockedOut,PasswordExpired,PasswordLastSet
```

### Step 4 — Review Authentication Logs

1. Open **Event Viewer**.
2. Navigate to **Windows Logs → Security**.
3. Select **Filter Current Log**.
4. Search for **Event ID 4625**, which records failed logon events.
5. Compare the event timestamp, account name, and logon details with the reported incident.

Check that the timestamps line up with when the user had trouble. Old failures, including your own testing, can look like evidence when they aren't.

### Step 5 — Perform an Authorized Password Reset

1. In Active Directory Users and Computers, right-click the account.
2. Select **Reset Password**.
3. Set a temporary password according to organizational policy.
4. Require a password change at next logon where appropriate.
5. Deliver temporary credentials through an approved secure channel.

### Step 6 — Verify Resolution

Have the employee sign in and confirm they can reach the applications they need.

If successful, record the verification and close the incident. Otherwise, continue troubleshooting or escalate.

## Escalation Criteria

Escalate when:

- The account continues failing authentication after authorized recovery.
- Domain controller connectivity appears unavailable.
- There is evidence of suspicious authentication activity.
- Account changes require elevated approval.
- The issue affects multiple employees.

## Security Considerations

Never include passwords, recovery codes, or confidential employee details in tickets or documentation.

## Related Ticket

[NSIT-1 — Employee Can't Sign In to Windows](../tickets/NSIT-1-windows-login.md)
