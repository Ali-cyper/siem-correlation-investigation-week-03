# Lab 06 — Dormant Implant

**Level:** Highest (two-day scenario)

## Scenario
There is **no brute force and no failed logon at all**. The account `sysadmin_backup` logs in cleanly on the first try, which points to credentials obtained earlier through a route outside the provided data (phishing, an earlier leak, or password reuse). A service is created immediately, then the implant stays dormant for 19 hours. A legitimate security scan in the data acts as the main distraction.

## Attack chain
1. Clean login on `sysadmin_backup` with no failed attempts.
2. Service installed immediately (4697).
3. Dormant for 19 hours.
4. PowerShell with double encoding: Base64 of UTF-16LE, containing an inner Base64 + gzip layer.

## Key pivots
| Type | Value |
|---|---|
| Account | `sysadmin_backup` |
| Pattern | Successful logon with zero failures beforehand |
| Event | 4697 (service installed) |
| Timing | 19 hours of dormancy after the service was created |
| Encoding | Base64 (UTF-16LE) → inner Base64 + gzip |

## Lessons
- The absence of failed attempts is itself evidence: the credentials were likely stolen earlier. This conclusion was reached independently.
- Separated the legitimate security scan from the real incident.
- When unsure whether any attempt had succeeded, went back and built an exact AND filter on `source.ip` + `event.code` instead of assuming. The next step is to make that verification automatic.
- Kept checking after about half an hour of trying.

## Analyst report
The original written report and verdict for this lab are not archived in this repo.
