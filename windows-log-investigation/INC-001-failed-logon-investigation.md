# INC-001 — Failed Logon Attempts (Event ID 4625)

- **Environment:** Active Directory lab, domain controller `DC01.quarm.local`
- **Log source:** Windows Security log, Event ID 4625
- **Activity date:** 6/25/2026 (lockout policy follow-up on 9/16/2026)
- **Investigator:** Quarm Adeniran

## Summary

I found six failed logon events (Event ID 4625) in the Security log for 6/25/2026. Five of them happened within about 25 minutes of each other, and I'd caused them on purpose: wrong passwords for `testuser` through `runas`, plus one attempt with a username that doesn't exist. The sixth event, from almost two hours earlier, looked different, because it was logged under a different computer name in `WORKGROUP` instead of the `QUARM` domain. After looking into it, I found it was just an old entry from before this VM was renamed and promoted to a domain controller. It wasn't a separate machine.

The more important finding was that none of the wrong passwords locked the account. I followed up by setting a lockout policy and testing it.

## Timeline (6/25/2026)

| Time | Account | What happened | Status / Sub-status | Computer |
|---|---|---|---|---|
| 5:25:57 PM | Not part of my testing (see below) | Bad password | 0xC000006D / 0xC000006A | WIN-BRQ06M4N1G8 (old hostname, WORKGROUP) |
| 6:48:12 PM | testuser (not confirmed) | Bad password | 0xC000006D / 0xC000006A | DC01.quarm.local |
| 7:11:54 PM | testuser | Bad password | 0xC000006D / 0xC000006A | DC01.quarm.local |
| 7:12:11 PM | testuser | Bad password | 0xC000006D / 0xC000006A | DC01.quarm.local |
| 7:12:22 PM | testuser | Bad password | 0xC000006D / 0xC000006A | DC01.quarm.local |
| 7:13:11 PM | notarealuser | User doesn't exist | 0xC000006D / 0xC0000064 | DC01.quarm.local |

For the 6:48:12 PM event, I didn't capture the "Account For Which Logon Failed" field. I've listed it as `testuser` because it matches the others (same domain, same codes, same machine), but I haven't confirmed that.

## How I investigated

1. Filtered the Security log for Event ID 4625, which returned six events.
2. Opened each one and recorded the time, account, status and sub-status, and computer.
3. Looked up the codes so I could tell the failures apart instead of assuming they were all the same. `0xC000006D` is the general "logon failed" status. The sub-status gives the reason: `0xC000006A` means the username was right but the password was wrong, and `0xC0000064` means the username doesn't exist.
4. Checked the logon type. The events I looked at showed **Logon Type 2** (interactive, credentials typed on the machine itself) rather than Type 3 (network). That fits, since I ran `runas` locally.
5. Followed up on the event that didn't fit. Its subject was `WIN-BRQ06M4N1G8$` in `WORKGROUP`, while the later events show `DC01$` in `QUARM`. That's this server's auto-generated name from before I renamed and promoted it.

## What I found

- The failures came from two accounts: `testuser` (wrong password) and `notarealuser` (doesn't exist).
- Three wrong-password attempts on `testuser` happened within 28 seconds (7:11:54 to 7:12:22), with the nonexistent-user attempt less than a minute later.
- The `WIN-BRQ06M4N1G8` event was the server's old identity, not another host.
- **No lockout ever happened.** Repeated bad passwords on the same account went through with no limit. In a real environment, that means someone could keep guessing passwords indefinitely.

## Recommendations

1. Set an account lockout policy so repeated bad passwords lock the account.
2. Alert on several failed logons for the same account in a short window, so this kind of pattern doesn't depend on someone spotting it in Event Viewer.

## Follow-up: account lockout policy

I went back and implemented recommendation 1.

**Change:** I created a GPO called `Account-Lockout-Policy` with a lockout threshold of 5 invalid attempts and a 30-minute lockout duration.

**Problem:** The policy didn't apply, even though the GPO was linked and enabled. I ran `gpresult /h` to see which GPO was winning each setting. It showed that the Default Domain Policy also defined the lockout threshold, set to 0, and was taking priority over my GPO. Domain account policies normally belong in the Default Domain Policy anyway, so I moved the settings there instead of fighting the precedence order. Then I ran `gpupdate /force`.

**Test:** On 9/16/2026, I repeated the `runas` wrong-password test against `testuser`. After five bad passwords, `runas` returned a different error: **1909: The referenced account is currently locked out and may not be logged on to.** Event Viewer recorded **Event ID 4740** (account locked out) for `testuser` at 4:52:15 PM.

**Cleanup:** I unlocked the account in Active Directory Users and Computers (Account tab, **Unlock account**). A help desk tech would do the same thing after confirming the lockout was user error and not an attack.

## Evidence

Screenshots for each step are in this folder's [README](README.md#screenshots).
