# Reference — Week 03

Quick reference for the events, ports and techniques that appeared in the labs. Definitions are general; lab-specific facts are in `cases/`.

## Windows events seen in the labs

| ID | Meaning | Where it appeared |
|---|---|---|
| 4648 | Logon attempted with explicit credentials | Lab 3 |
| 4698 | Scheduled task created | Lab 3 |
| 4720 | User account created | Lab 4 |
| 4732 | Member added to a security-enabled local group | Lab 4 (Administrators) |
| 1102 | Audit (Security) log cleared | Lab 4 |
| 4697 | Service installed on the system | Labs 5, 6 |
| 4672 | Special privileges assigned to a new logon (automatic; not an escalation command) | Lesson learned, see mistake-log |

## Ports

| Port | Service | Lab |
|---|---|---|
| 5985 | WinRM (HTTP) | 2 |
| 1433 | Microsoft SQL Server | 4 |

## Decoding PowerShell `-enc`

`-EncodedCommand` is Base64 of a **UTF-16LE** string.

- **One layer (Labs 1–4):** CyberChef → `From Base64` → `Decode text` (UTF-16LE).
- **Lab 5 pattern:** after the first decode, an inner Base64 string remains → `From Base64` again.
- **Lab 6 pattern:** after the first decode, the inner string is Base64 of gzip data → `From Base64` → `Gunzip`.

If the output is still unreadable, look for another layer before assuming the payload is junk.

## Kibana pattern that settled a doubt (Lab 6)

Combine the source and the event type in one query instead of assuming:

```
source.ip : "<ip>" and event.code : "<id>"
```

Replace the placeholders with values copied from the data.

## Habits that came out of the week

1. Check the timezone of every source before correlating times.
2. Pivot on `IP / Host / User / Timestamp`, and use more than one independent piece of evidence.
3. Read TCP flags inside the whole flow, never alone.
4. The first compromised account is not always the target.
5. Distinguish beaconing from exfiltration by size and direction.
6. Copy-paste names and IPs; verify hostnames character by character.
7. Before concluding, check: entry, persistence, time gaps, and whether there is a second incident.

## Response order used in the reports

Isolate → Block → Remove persistence → Investigate the entry point.
