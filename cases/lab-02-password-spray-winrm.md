# Lab 02 — Password Spray over WinRM

**Level:** Beginner+

## Scenario
The authentication pattern changes from one targeted account (Lab 1) to one password tried across several accounts, over WinRM on port 5985. Access succeeded on `svc_backup`, followed by encoded PowerShell, and the scenario also includes DNS exfiltration.

## Attack chain
1. Password spray across multiple accounts via WinRM (5985).
2. Successful access on `svc_backup`.
3. PowerShell executed with `-enc` (one Base64 layer).
4. DNS exfiltration.

**Persistence:** none observed.

## Key pivots
| Type | Value |
|---|---|
| Technique | Password spray |
| Protocol / port | WinRM / 5985 |
| Account (success) | `svc_backup` |
| Execution | PowerShell `-enc`, single layer |

## Lesson
`RST` does not automatically mean "connection failed". The meaning depends on the full flow and on what happened before and after. See [mistake-log](../mistake-log.md), item 1.

This lab was finished faster than Lab 1.

## Analyst report
The original written report and verdict for this lab are not archived in this repo.
