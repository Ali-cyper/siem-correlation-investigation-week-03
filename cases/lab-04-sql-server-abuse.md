# Lab 04 — SQL Server Abuse

**Level:** Intermediate+ (anti-forensics)

## Scenario
An exposed database service is attacked directly. The compromised account, `sql_svc`, was already privileged. The attacker creates a new account, grants it administrative rights, and then tries to clear the log.

## Attack chain
1. Brute force against MSSQL on port 1433.
2. Access with the privileged account `sql_svc`.
3. PowerShell executed with `-enc` (one Base64 layer).
4. New account created (4720) and added to Administrators (4732).
5. Attempt to clear the Security log (1102).

The order above follows the attack description; exact timestamps are not archived.

## Key pivots
| Type | Value |
|---|---|
| Service / port | MSSQL / 1433 |
| Account | `sql_svc` (privileged from the start) |
| Events | 4720, 4732, 1102 |
| Execution | PowerShell `-enc`, single layer |

## Lesson
Port 1433 ties the incident to MSSQL but is context, not proof by itself. A privileged service account changes how far the access reaches. Event 1102 is anti-forensics behaviour and should be treated as part of the chain.

## Session note
Kept checking work despite fatigue. The session ended early on day 2 because of a lab data-generation issue (since fixed) and tiredness.

## Analyst report
The original written report and verdict for this lab are not archived in this repo.
