# INC-001 — Repeated Failed Authentication Attempts (Event ID 4625)

**Environment:** Active Directory Help Desk Lab — domain controller `DC01.quarm.local`
**Log source:** Windows Security Event Log, Event ID 4625
**Date of activity:** 6/25/2026
**Investigator:** Quarm Adeniran

> Note: the account name attempted in the 6:48:12 PM event is inferred (same domain, same failure code, and contiguous with the confirmed `testuser` cluster) rather than directly confirmed on-screen — low-risk assumption, but worth a final glance if you want it airtight.

---

## Executive Summary

Six Event ID 4625 (failed logon) entries were identified in the Security log on 6/25/2026. Five were clustered within a ~25-minute testing window and are attributable to intentional test activity (`runas` attempts against a valid account with a wrong password, and against a non-existent account). A sixth event, timestamped nearly two hours earlier, showed a different Subject account domain (`WORKGROUP` vs. `QUARM`) and machine account (`WIN-BRQ06M4N1G8$` vs. `DC01$`) than the other five. This is consistent with the Security log retaining an entry from before this VM was renamed and promoted from its default hostname to the domain controller `DC01.quarm.local` — not a separate or unexpected host, just older history on the same machine. It's treated as out of scope for this investigation rather than part of the tested activity. No account lockout occurred at any point in the in-scope cluster, despite five consecutive bad-password attempts against the same account.

## Timeline

| Time (6/25/2026) | Account | Result | Status / Sub Status | Source Host |
|---|---|---|---|---|
| 5:25:57 PM | *out of scope — see note below* | Bad password | 0xC000006D / 0xC000006A | WIN-BRQ06M4N1G8 (WORKGROUP — pre-promotion) |
| 6:48:12 PM | testuser *(inferred)* | Bad password | 0xC000006D / 0xC000006A | DC01.quarm.local (Subject: DC01$ / QUARM) |
| 7:11:54 PM | testuser | Bad password | 0xC000006D / 0xC000006A | DC01.quarm.local |
| 7:12:11 PM | testuser | Bad password | 0xC000006D / 0xC000006A | DC01.quarm.local |
| 7:12:22 PM | testuser | Bad password | 0xC000006D / 0xC000006A | DC01.quarm.local |
| 7:13:11 PM | notarealuser | Account doesn't exist | 0xC000006D / 0xC0000064 | DC01.quarm.local |

**Logon Type observed:** 2 (Interactive) — confirms these were local/console-style attempts rather than network-based (Type 3) authentication, consistent with the simulated `runas` testing rather than a remote intrusion attempt.

## Indicators of Compromise (IOCs) / Notable Artifacts

- **Target account(s):** `testuser`, `notarealuser`
- **Pre-promotion host artifact:** `WIN-BRQ06M4N1G8$` / domain `WORKGROUP` — traced to this VM's default hostname and workgroup state prior to domain promotion; not a separate or external host
- **Failure pattern:** 4 consecutive bad-password attempts against the same account (`testuser`) within a ~25-second span (7:11:54–7:12:22 PM), followed by a username-enumeration-style attempt against a nonexistent account

## Impact Assessment

No successful authentication followed these failures, and no account lockout was triggered. In a production environment, the lack of a lockout after 4+ consecutive bad-password attempts on one account would represent a real exposure — it means brute-force attempts against this account are not currently self-limiting.

## What Was Done

1. Filtered the Security log for Event ID 4625 (Filter Current Log → Event ID 4625), returning 6 matching events.
2. Opened each event's General tab and recorded timestamp, account name (where visible), Status/Sub Status code, and source host.
3. Cross-referenced the failure codes against their meanings — `0xC000006A` (bad password) vs. `0xC0000064` (account does not exist) — to distinguish attack/testing intent per event rather than treating all six as identical.
4. Identified one event (5:25:57 PM) as inconsistent with the rest of the cluster based on timing and source host, then checked its Subject fields (Account Name, Account Domain) to confirm the cause rather than assuming it was part of the same activity.

## Recommendations

1. **(Resolved during investigation)** The 5:25:57 PM event was traced to this VM's pre-promotion identity (`WIN-BRQ06M4N1G8$` / `WORKGROUP`) rather than an unrelated host — included here to show the anomaly was chased down and explained, not just noticed and set aside.
2. **Review and enforce an account lockout policy** (e.g., lock after 5 bad attempts within 15 minutes) — none of the observed attempts triggered a lockout, meaning the account is not currently protected against sustained password-guessing.
3. **Consider alerting on repeated 4625 events against a single account within a short window** — this same pattern (4 failures in under 30 seconds) is exactly the kind of signal a SIEM detection rule should flag automatically rather than requiring manual log review.

---
*Screenshots referenced in this investigation: see `/evidence` in this folder.*
