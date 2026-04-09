# Project Sentinel: Automated Vulnerability Audit & System Hardening

## 🎯 Executive Summary
This project demonstrates a complete Security Lifecycle—from automated discovery to tactical remediation. I developed a custom Bash-based auditing tool to identify network exposures and implemented industry-standard hardening techniques to secure a Linux environment.

---

## 🛠️ Phase 1: Tool Development & Logic
Before performing the audit, I developed **sentinel_report.sh**. This script automates the analysis of Nmap scan data, using string-matching logic to categorize services into risk levels ([CRITICAL], [WARNING], or [SAFE]).

**Key Activities:**
* **Scripting:** Used `grep` and `if-else` loops to parse service versions.
* **Risk Mapping:** Defined Port 80 as a "Warning" (unencrypted) and Port 3306 as "Critical" (exposed database).

![Screenshot 1: source code analysis](Sentinel_01.jpeg)

---

## 🕵️ Phase 2: Vulnerability Discovery (The "Before" State)
Using a "Blind Scan" approach, I performed a full-range reconnaissance on the target system to identify active services without prior knowledge of the configuration.

**Commands Executed:**
* `nmap -sV -T4 -oN initial_scan.txt localhost`: Scanned the system for service versions and saved the output.
* `./sentinel_report.sh`: Executed the custom auditor against the raw scan data.

**Findings:** The audit revealed an **Apache Web Server (Port 80)** and a **MariaDB Database (Port 3306)** openly listening for connections.

![Screenshot 2: initial vulnerability report](Sentinel_02.jpeg)

---

## 🛡️ Phase 3: Tactical Remediation & Hardening
Once the risks were identified, I transitioned to the role of a Security Engineer to "close the doors" and harden the system perimeter.

**Commands Executed:**
* `sudo apt install ufw`: Installed the Uncomplicated Firewall.
* `sudo ufw deny 3306/tcp`: Configured a firewall rule to drop all incoming traffic to the database port.
* `sudo systemctl stop apache2`: Decommissioned the unencrypted web service to eliminate the attack surface.

![Screenshot 3: system hardening actions](Sentinel_03.jpeg)

---

## 🔄 Phase 4: Tool Iteration & Maintenance
In real-world security, tools must be updated to reflect new data. I modified the script to point toward the verification scan results, ensuring the "Post-Fix" audit was accurate.

**Activities:**
* **Maintenance:** Updated the `SCAN_FILE` variable within the script logic.
* **Version Control:** Demonstrated the ability to modify automation scripts on the fly.

![Screenshot 4: script update for verification](Sentinel_04.jpeg)

---

## ✅ Phase 5: Final Validation (The "After" State)
The final step was to prove the effectiveness of the remediation. I performed a final "Verification Scan" to confirm that the changes were correctly applied and that no vulnerabilities remained.

**Commands Executed:**
* `nmap -sV -oN verified_scan.txt localhost`: Confirmed the services were no longer reachable.
* `./sentinel_report.sh`: Produced a clean audit report.

**Result:**
The system achieved a **Zero-Exposure** state, with the script reporting **[SAFE]** for all checked parameters.

![Screenshot 5: final security verification](Sentinel_05.lpeg)
