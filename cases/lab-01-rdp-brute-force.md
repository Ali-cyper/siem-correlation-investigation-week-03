# Lab 01 — RDP Brute Force

**Level:** Beginner

## Scenario
Repeated failed logon attempts against the account `svc_helpdesk` over RDP, coming from an internal host described as compromised. Encoded PowerShell appears in the evidence.

## Attack chain
1. Repeated failed RDP logons against `svc_helpdesk` from a compromised internal host.
2. PowerShell executed with `-enc` (one Base64 layer).

**Persistence:** none observed.

## Key pivots
| Type | Value |
|---|---|
| Account | `svc_helpdesk` |
| Protocol | RDP |
| Execution | PowerShell `-enc`, single layer |

## Lesson
Assumed that `RST` always means a failed connection. Lab 2 was built to break that rule. See [mistake-log](../mistake-log.md), item 1.

## Analyst report
The original written report and verdict for this lab are not archived in this repo.
