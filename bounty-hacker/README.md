# Bounty Hacker — Walkthrough

**Author:** Tiago D.  
**Room:** Bounty Hacker (TryHackMe)  
**Goal:** Obtain the sensitive root file.

---

## Summary
Short chain: anonymous FTP → found password file → SSH login → sudo escalation to root.

---

## How to read this walkthrough
- Screenshots are in `screenshots/`.  
- Outputs and credentials are redacted.  
- This is a learning/walkthrough document, not an exploit repo.

---

## Recon
**What I did:** port scan and service enumeration.

![Port scan results](screenshots/recon-01.png)  
*Figure 1 — Nmap scan showing open FTP, SSH and HTTP ports.*

**Notes:** The FTP service was accessible anonymously which led to further discovery.

---

## FTP: anonymous access
![FTP listing](screenshots/ftp-listing-01.png)  
*Figure 2 — Anonymous FTP directory listing. A file named `passwords.txt` was present.*

**Explanation:** The listing contained a small file. I downloaded it and inspected its contents (redacted below).

---

## Using found credentials (SSH)
![SSH login](screenshots/ssh-login-01.png)  
*Figure 3 — Successful SSH login using recovered credentials.*

**Explanation:** Credentials from the FTP file allowed SSH access to the user account `exampleuser`. From there I enumerated local files and permissions.

---

## Privilege escalation
![Sudo -l output](screenshots/sudo-l-01.png)  
*Figure 4 — `sudo -l` output showing a binary allowed without password.*

**Explanation:** The user can run `/usr/bin/somebinary` via sudo with NOPASSWD. That binary has an unsafe SUID/behavior that allows escalation. I used safe, documented GTFOBins techniques to escalate.

---

## Root proof
![Root file view](screenshots/root-file-01-redacted.png)  
*Figure 5 — Redacted view of the sensitive file as proof of root access.*

**Notes:** Screenshot redacted to remove sensitive content.

---

## Mitigations and recommendations
- Disable anonymous FTP.  
- Restrict `sudo` entries and avoid NOPASSWD where unnecessary.  
- Enforce strong authentication and rotation of credentials.  
- Monitor access logs for suspicious file downloads.

---

## Files included
- `report.pdf` — Full written report.  
- `screenshots/` — All screenshots used in this walkthrough.  
- `ATTACK-mapping.md` — MITRE ATT&CK mapping.  
- `recommendations.md` — Detailed mitigations.

---

## Final notes
This walkthrough is intended for learning and defensive improvement. Do not use these steps for unauthorized access.
