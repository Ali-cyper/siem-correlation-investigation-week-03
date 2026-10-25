# Mistake Log — Week 03

Mistakes made during the SIEM correlation labs, what corrected them, and the habit that came out of each.
"Lab" is filled in only where the mistake is tied to a specific lab; otherwise it is listed as Week 3.

## Resolved

| # | Lab | Mistake | Correction | Lesson |
|---|---|---|---|---|
| 1 | 1 → 2 | Assumed `RST` always means the connection failed | Lab 2 deliberately broke the rule | Read the whole flow and surrounding events; never judge from one TCP flag |
| 2 | Week 3 | Treated event 4672 like `sudo su` (mixing Windows and Linux) | 4672 is an automatic record of special privileges assigned to a logon, not an escalation action | Don't map Windows events onto Linux commands |
| 3 | Week 3 | Kibana and PCAP times looked hours apart | Cause was local display time vs raw UTC | Check timezone first, before deciding two events don't line up |
| 4 | Week 3 | Mixed up C2 beaconing and data exfiltration | Distinguished by data size and direction | Look at volume and direction before naming the behaviour |
| 5 | Week 3 | Confused `SRV-FILE01` with `SRV-FILE02` | Compare hostnames character by character | Verify the number, not just the name |

## Still open

| # | Lab | Mistake | Fix to apply |
|---|---|---|---|
| 6 | Week 3 | Retyped names/IPs with small errors (`203.0.113.201` written as `203.0.113.31`; `WinDefragScheduler` written as `winDefragScheduler`) | Always copy-paste from the source. One wrong character in an IP sends responders to the wrong host |
| 7 | Week 3 | Reports missed whole elements (a persistence step, a time gap, a second incident in the data) until asked directly | Go through the full checklist before writing any conclusion |
| 8 | 6 | Said "not sure whether any attempt succeeded" and waited, instead of verifying | Done once (AND filter on `source.ip` + `event.code`); make it automatic |
| 9 | Week 3 | Small spelling slips in technical English | Proofread before publishing |
