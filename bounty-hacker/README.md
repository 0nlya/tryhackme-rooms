# TryHackMe — Bounty Hacker (Walkthrough)

**Author:** Tiago D.  
**Type:** Capture the Flag / Room walkthrough  
**Summary:** Short chain: anonymous FTP → password list → SSH bruteforce → sudo escalation → root read.  
(Mapping to MITRE in `ATTACK-mapping.md`.)

## TL;DR
- Lab objective: obtain a sensitive file as root.
- Results: SSH access with obtained credentials, escalation to root via SUID/NOPASSWD.  
- Main mitigations: disable anonymous FTP, enforce strong authentication, audit sudoers.

## What I did (high level)
1. Recon: port scan, identification of FTP/SSH/HTTP.  
2. Access: anonymous FTP listing → found file containing credentials.  
3. Remote access: used credentials to SSH.  
4. Escalation: checked `sudo -l` and abused SUID/GTFOBins.

> Note: This repository contains a report and screenshots. It does not include working exploits or any published credentials.

## Files
- `report.pdf` — full report.  
- `screenshots/` — visual evidence.  
- `ATTACK-mapping.md` — MITRE ATT&CK mapping.  
- `recommendations.md` — mitigations and fixes.

## Lessons learned
- Do not allow anonymous FTP.  
- Monitor logs and apply restrictive sudo policies.  
- Use key-only SSH.

## License
This project is released under the MIT License.
