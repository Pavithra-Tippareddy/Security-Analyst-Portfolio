# Security Analyst Portfolio — Pavithra Tippareddy

Hands-on SOC Analyst labs showing Windows event logging, Splunk detections, and network monitoring.

## 🔹 Lab Goals
- Generate real security events (failed logins, PowerShell, Nmap scans, ICMP traffic).
- Ingest logs into Splunk for detection.
- Document findings like a SOC Analyst.

## 🔹 Repo Structure
- **/setup** → Configuring Windows auditing, Splunk inputs, Sysmon.
- **/labs** → Step-by-step exercises (4625 failed logins, 4104 PowerShell logs, Nmap/ICMP scans).
- **/splunk_queries** → SPL queries used in labs.
- **/writeups** → Analyst-style incident reports.
- **/screenshots** → Evidence from Event Viewer, Splunk dashboards, Wireshark.

## 🔹 Next Steps
- Add Sysmon detections (4688).
- Add brute-force login detection (4740).
- Expand Splunk correlation rules.

## Labs Completed
1. [Failed Logins Detection](writeups/failed_logins.md)
2. [Nmap & ICMP Analysis](writeups/nmap_icmp.md)

Screenshots for each lab are stored in the `screenshots/` folder.

## TryHackMe SOC Simulation – Phishing Email Investigation.
  * Investigated a simulated phishing alert using Splunk SIEM. Reviewed email indicators, searched firewall/proxy logs, and produced an        incident case report confirming a true positive with no user compromise.  

 
 ## 🧪 SOC Simulations Summary
Completed multiple SOC analyst simulations on TryHackMe using Splunk SIEM to triage and document different alert types:

- Phishing Email Investigation ✅ *(detailed write-up below)*
- Brute Force Login Detection
- Malware Alert Escalation
- Data Exfiltration Attempt
- Suspicious PowerShell Execution

* Each scenario strengthened skills in alert triage, log correlation, and incident documentation.

## [Detailed Write-up: Phishing Email Investigation](./writeups/tryhackme_soc_simulation_phishing_investigation.md)


