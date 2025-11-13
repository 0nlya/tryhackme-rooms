# MR ROBOT — Walkthrough

**Author:** Tiago Dias  
**Room:** MR ROBOT (TryHackMe)  
**Goal:** Obtain the root flag and recover all key fragments.

---

## Summary
Recon → Web enumeration → Hidden content discovery (`robots.txt`) → Decode credentials → Foothold → Reverse shell → Stabilization → Local enumeration → Privilege escalation (GTFOBins / misconfigured binaries) → Root flag.

---

## How to read this walkthrough
- Screenshots are in `screenshots/`.  
- Outputs and credentials are redacted.  
- This is a learning walkthrough, not an exploit repository.

---

# Recon

**What I did:** Full port scan and service enumeration.

![Nmap scan](screenshots/01_nmap_scan.png)  
*Figure 1 — Nmap showing exposed services for exploration.*

![Website check](screenshots/02_website.png)  
*Figure 2 — Initial HTTP view of the MR Robot web application.*

![Gobuster scan](screenshots/03_Gobuster_scan.png)  
*Figure 3 — Gobuster revealing hidden directories and files.*

**Notes:** The enumeration revealed hidden paths containing useful information.

---

# Web enumeration

![robots.txt](screenshots/04_robots_key.png)  
*Figure 4 — robots.txt leaking hidden key paths.*

![Key fragment](screenshots/05_key_1.png)  
*Figure 5 — First key fragment obtained.*

![Dictionary](screenshots/06_dictionary.png)  
*Figure 6 — Wordlist/dictionary discovered for future credential attempts.*

---

# Encoded content & credential discovery

![Login page](screenshots/07_loginpage.png)  
*Figure 7 — Application login form.*

![License page](screenshots/08_license_page.png)  
*Figure 8 — License page containing encoded information.*

![Base64 string](screenshots/09_base64.png)  
*Figure 9 — Extracted base64-encoded string.*

![Decoded credentials](screenshots/10_credentials.png)  
*Figure 10 — Credentials recovered after decoding.*

**Explanation:** The recovered credentials allowed initial authenticated access.

---

# Foothold & Reverse Shell

![Reverse shell setup](screenshots/11_revshell.png)  
*Figure 11 — Reverse shell payload preparation.*

![Reverse shell access](screenshots/12_revshell_acess.png)  
*Figure 12 — Successful reverse shell connection.*

![Shell stabilization](screenshots/13_stabilize_shell.png)  
*Figure 13 — Stabilizing the shell using Python pty.*

---

# Local enumeration & user credentials

![Robot user hints](screenshots/14_robot_credentials.png)  
*Figure 14 — Files containing the robot user clues.*

![Robot password](screenshots/15_robot_password.png)  
*Figure 15 — Password discovered enabling user pivoting.*

![Key part 2](screenshots/16_key_2.png)  
*Figure 16 — Second key fragment found.*

---

# Privilege escalation

![Privilege escalation vector](screenshots/17_privilege_escalation.png)  
*Figure 17 — Enumeration of escalation methods.*

![GTFOBins exploit](screenshots/18_gtfobins.png)  
*Figure 18 — Privilege escalation using GTFOBins technique.*

![Nmap interactive shell](screenshots/19_nmap_exploit.png)  
*Figure 19 — Alternative escalation using nmap interactive shell.*

---

# Root proof & final key

![Root flag](screenshots/20_key_3.png)  
*Figure 20 — Final key fragment / root flag.*

---

# Mitigations & recommendations

- Do not expose sensitive paths in `robots.txt`.  
- Avoid storing encoded credentials in public files.  
- Remove unnecessary SUID binaries and restrict sudo permissions.  
- Enforce strict file permissions and access controls.  
- Monitor server logs for anomalies and brute-force attempts.  

---

# Included files

- `screenshots/` — All screenshots.  
- `Walkthrough.md` — This walkthrough.

---

# Final notes
This walkthrough is intended for educational and defensive purposes only. Unauthorized access is illegal.
