# Windows Failed Login Investigation

## Scenario
A series of failed authentication events was reviewed in a local Windows environment to practice basic security log analysis and incident triage.

## Environment
- Windows Event Viewer
- Windows Security Log
- Local Windows workstation

## Evidence Reviewed
- Security Event ID: 4625
- Event category: Logon
- Audit result: Audit Failure
- Number of filtered events reviewed: 5
- Relevant process observed: `C:\Windows\System32\svchost.exe`

## Findings
Multiple Event ID 4625 records were identified in the Windows Security log. Event ID 4625 indicates that an account failed to log on.

The reviewed event showed:
- Failure reason: An error occurred during logon
- Status code: `0xC000006D`
- Sub-status code: `0xC0000380`
- Logon activity was recorded as an audit failure

## Initial Assessment
The events were generated in a controlled local learning environment. No evidence was identified that the activity originated from an external attacker.

Repeated Event ID 4625 events in a production environment could indicate:
- Incorrect password attempts
- Misconfigured services or scheduled tasks
- A locked or disabled account
- Brute-force or password-spraying activity

## Recommended Response
1. Confirm whether the authentication attempts were expected.
2. Review the affected account and recent password changes.
3. Check for repeated failures across multiple accounts or devices.
4. Review account lockout policies and authentication controls.
5. Escalate for further investigation if the activity is unexpected or continues.

## Skills Demonstrated
Windows Event Viewer, Security Event Log review, authentication monitoring, Event ID 4625 analysis, basic incident triage, and technical documentation.
