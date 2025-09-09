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

