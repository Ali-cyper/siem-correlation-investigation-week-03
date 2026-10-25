# Lab 03 — Lateral Movement

**Level:** Intermediate (two hosts instead of one)

## Scenario
The incident is no longer limited to a single machine. The attacker starts with a low-privilege account and then moves to a privileged account on a second host using explicit credentials.

## Attack chain
1. Brute force on a low-privilege account.
2. Logon with explicit credentials (event 4648) to a privileged account on a second host.
3. PowerShell executed with `-enc` (one Base64 layer).
4. Scheduled Task created for persistence (event 4698).

## Key pivots
| Type | Value |
|---|---|
| Event | 4648 (explicit credentials) |
| Event | 4698 (scheduled task created) |
| Movement | Between two hosts, low-privilege account to privileged account |
| Execution | PowerShell `-enc`, single layer |

## Lesson
The first compromised account is not always the final target. Build the timeline across both hosts, not one.

## Notes
PCAP pivoting, Kibana pivoting and CyberChef decoding were done independently in this lab.

## Analyst report
The original written report and verdict for this lab are not archived in this repo.
