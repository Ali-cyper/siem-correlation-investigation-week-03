# Lab 05 — LOLBin Abuse

**Level:** Advanced

## Scenario
A slow, spaced-out brute force against `fin_svc` that is easy to miss, followed by a new service and a double-encoded PowerShell payload. The data also contains a second, unrelated incident, included as a discrimination exercise.

## Attack chain
1. Low-and-slow brute force on `fin_svc`.
2. Service installed for persistence (4697).
3. PowerShell with double encoding: Base64 of UTF-16LE, containing an inner Base64 layer.

## Key pivots
| Type | Value |
|---|---|
| Account | `fin_svc` |
| Pattern | Low-and-slow brute force (attempts spaced out in time) |
| Event | 4697 (service installed) |
| Encoding | Base64 (UTF-16LE) → inner Base64 |

## Lessons
- Slow attempts still form a pattern; widen the time window when looking for brute force.
- Distinguished the real incident from the unrelated one using failure pattern, lack of correlation, and lack of success.
- Found the second decoding layer independently or with minimal guidance.

## Analyst report
The original written report and verdict for this lab are not archived in this repo. The specific living-off-the-land binary used in the scenario is also not recorded.
