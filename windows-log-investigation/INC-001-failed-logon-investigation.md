# INC-001 — Failed Logon Attempts (Event ID 4625)

**Environment:** Active Directory Help Desk Lab — domain controller `DC01.quarm.local`
**Log source:** Windows Security Event Log, Event ID 4625
**Date of activity:** 6/25/2026
**Investigator:** Quarm Adeniran

> Quick note: for the 6:48:12 PM event, I'm assuming the account was `testuser` since it matches the others (same domain, same error code, right next to them in time) — I didn't reopen that specific event to double-check the account name field, so worth confirming if you want to be fully sure.

---

## Summary

I found 6 failed logon events (Event ID 4625) in the Security log from 6/25/2026. Five of them happened close together, within about 25 minutes, and came from tests I ran on purpose — using the `runas` command with a wrong password a few times, and once with a username that doesn't exist. But one event, from almost two hours earlier, looked different: it was tied to a different computer account and domain (`WORKGROUP` instead of `QUARM`). I looked into why, and it turned out to just be an old log entry from before this VM was renamed and promoted to be the domain controller — not a separate machine, just leftover history from earlier in the build. I also noticed that none of my failed attempts actually locked the account, even after several wrong passwords in a row on the same user.

## Timeline

| Time (6/25/2026) | Account | What Happened | Status / Sub Status | Computer |
|---|---|---|---|---|
| 5:25:57 PM | *not part of my testing — see note* | Bad password | 0xC000006D / 0xC000006A | WIN-BRQ06M4N1G8 (WORKGROUP — old hostname, pre-promotion) |
| 6:48:12 PM | testuser (assumed) | Bad password | 0xC000006D / 0xC000006A | DC01.quarm.local (DC01$ / QUARM) |
| 7:11:54 PM | testuser | Bad password | 0xC000006D / 0xC000006A | DC01.quarm.local |
| 7:12:11 PM | testuser | Bad password | 0xC000006D / 0xC000006A | DC01.quarm.local |
| 7:12:22 PM | testuser | Bad password | 0xC000006D / 0xC000006A | DC01.quarm.local |
| 7:13:11 PM | notarealuser | Account doesn't exist | 0xC000006D / 0xC0000064 | DC01.quarm.local |

One more thing I checked: the Logon Type on these events was **2**, which means Interactive (like typing credentials in directly) rather than 3 (Network). That fits, since I ran these tests locally with `runas` rather than trying to log in remotely.

## What I Found

- The two accounts I tested against: `testuser` and `notarealuser`
- One event that looked odd at first — `WIN-BRQ06M4N1G8` in domain `WORKGROUP` — turned out to just be this VM's old identity from before it became the domain controller, not a separate host
- 4 wrong-password attempts on `testuser` happened within about 25 seconds of each other, then one attempt on a username that doesn't exist right after

## Why It Matters

None of these attempts actually got in, which is good, but I also never saw a lockout happen, even after 4 wrong passwords in a row on the same account. In a real environment, that's worth flagging — it means someone could keep guessing passwords without ever getting blocked.

## What I Did

1. Filtered the Security log for Event ID 4625, which pulled up 6 matching events.
2. Opened each one and wrote down the time, account name, status/sub-status code, and which computer it came from.
3. Looked up what the status codes actually meant — `0xC000006A` = wrong password, `0xC0000064` = account doesn't exist — so I could tell the attempts apart instead of assuming they were all the same thing.
4. Noticed one event didn't match the pattern of the rest and checked its details until I figured out why (the pre-promotion hostname, above).

## What I'd Recommend

1. Set up an account lockout policy (e.g., lock the account after 5 bad password attempts within 15 minutes) — right now nothing stops someone from just guessing passwords over and over.
2. It'd be worth setting up an alert for this kind of pattern (several failed logins on the same account in a short window) instead of having to notice it manually in Event Viewer, like I did here.

---
*Screenshots referenced in this investigation: see `/evidence` in this folder.*
