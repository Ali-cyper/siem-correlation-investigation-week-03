# Week 03 — SIEM Correlation Labs (Windows Logs + PCAP)

Part of a self-designed 12-week SOC investigation curriculum.
Week 1 covered Windows event logs, Week 2 covered PCAP analysis. Week 3 moves from reading single artifacts to **correlating evidence across sources** (Windows events in Elastic/Kibana, PCAP traffic, and decoded PowerShell) to rebuild a full attack chain.

> العربية: [README.AR.md](README.AR.md)

---

## Scope

- **6 labs**, increasing in difficulty from beginner to advanced.
- **Data sources:** Windows event logs in Elastic/Kibana, PCAP traffic, and PowerShell payloads decoded with CyberChef.
- **Core skill:** pivoting across `IP / Host / User / Timestamp` to connect events into one story.
- All datasets are **synthetic training scenarios**. No real victim data is used.

## Lab overview

| # | Scenario | Entry | Persistence | Obfuscation | Level |
|---|---|---|---|---|---|
| 1 | [RDP Brute Force](cases/lab-01-rdp-brute-force.md) | Repeated failed RDP logons on `svc_helpdesk` from a compromised internal host | None | PowerShell `-enc` (1 layer) | Beginner |
| 2 | [Password Spray over WinRM](cases/lab-02-password-spray-winrm.md) | Spray across accounts via WinRM (5985); success on `svc_backup` | None | PowerShell `-enc` | Beginner+ |
| 3 | [Lateral Movement](cases/lab-03-lateral-movement.md) | Brute force on a low-privilege account, then explicit-credential logon (4648) to a privileged account on a second host | Scheduled Task (4698) | PowerShell `-enc` | Intermediate |
| 4 | [SQL Server Abuse](cases/lab-04-sql-server-abuse.md) | Brute force on MSSQL (1433); `sql_svc` already privileged | New account + Administrators group (4720 / 4732) | PowerShell `-enc` + log-clearing attempt (1102) | Intermediate+ |
| 5 | [LOLBin Abuse](cases/lab-05-lolbin-abuse.md) | Low-and-slow brute force on `fin_svc` | New service (4697) | Double encoding (Base64 of UTF-16LE, then inner Base64) | Advanced |
| 6 | [Dormant Implant](cases/lab-06-dormant-implant.md) | Clean login with **no failed attempts** on `sysadmin_backup` | Immediate service (4697), then 19 hours dormant | Double encoding (Base64 of UTF-16LE, then Base64 + gzip) | Highest |

## How the labs progressed

- **Entry method:** weak/shared passwords over remote-admin protocols (Labs 1–2) → lateral movement where the first compromised account was not the final target (Lab 3) → an exposed database service with an already-privileged account (Lab 4) → slow brute force that is hard to spot (Lab 5) → no brute force at all, so credentials must have been obtained earlier through some other route (Lab 6).
- **Decoding:** one Base64 layer in Labs 1–4, then two different layered encodings in Labs 5 and 6.
- **Noise:** Labs 5–6 added decoy activity (a second unrelated incident, adware-type activity, a legitimate security scan) to practice separating real from benign.
- **Response plan used in the reports:** isolate → block → remove persistence → investigate the entry point.

## What improved

- Pivoting across IP / Host / User / Timestamp became more accurate and faster from lab to lab.
- Moved from single-layer to multi-layer decoding, mostly finding the right method independently or with very light hints.
- Correctly separated real incidents from decoys using failure patterns, lack of correlation, and lack of success.
- In Lab 6, when unsure whether any attempt succeeded, went back and built an exact AND filter (`source.ip` + `event.code`) instead of assuming.

## Still being worked on

- **Copy accuracy:** names and IPs must be copy-pasted from the source, not retyped.
- **Completeness:** review the full chain (persistence, time gaps, a second incident) before writing a conclusion.
- **Verify before concluding:** turn "I'm not sure" into a verification step automatically.
- **Technical English:** proofread spelling before publishing.

Full list in [mistake-log.md](mistake-log.md).

## Repository structure

```
.
├── README.md
├── README.AR.md
├── mistake-log.md
├── reference.md
├── cases/
│   ├── lab-01-rdp-brute-force.md
│   ├── lab-02-password-spray-winrm.md
│   ├── lab-03-lateral-movement.md
│   ├── lab-04-sql-server-abuse.md
│   ├── lab-05-lolbin-abuse.md
│   └── lab-06-dormant-implant.md
└── templates/
    ├── investigation-report.md
    └── timeline.md
```

## Limits of this repo

This write-up documents each scenario at the level of attack chain, key event IDs, accounts, ports and lessons. The raw datasets, exact timestamps, per-lab written verdicts and decoded payload text were not archived, so they are not reproduced here.
