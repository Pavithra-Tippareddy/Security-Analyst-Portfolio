# TryHackMe SOC Simulation – Phishing Email Investigation

**Date Completed:** October 22, 2025  
**Platform:** [TryHackMe SOC Simulation (Public Summary)](https://tryhackme.com/soc-sim/public-summary/f0b88796daa1d9b9a38cc3d5b879096f8c09309121110082775588fb3a9900fe14915cc9049f839059deb584a254b4e4)  
**Tools Used:** Splunk (SIEM), Email Analysis, Threat Intelligence Lookup  

---

## 🧠 Objective
Investigate an alert for an inbound phishing email containing a suspicious shortened URL.  
Determine if any internal users accessed the malicious link, and classify the incident based on findings.

---

## 🔍 Investigation Summary

1. **Email Alert Review**
   - **Sender:** `urgents@amazon.biz`  
   - **Recipient:** `h.harris@thetrydaily.thm`  
   - **Subject:** “Your Amazon Package Couldn’t Be Delivered – Action Required”  
   - **Suspicious URL:** `http://bit.ly/3sHkX3da12340`

2. **Splunk Log Search**
   - Queried across all available indexes for `"bit.ly"` and the shortened link.
   - No hits found in firewall, proxy, or DNS logs.
   - Indicates the user did **not click** the link.

3. **Classification**
   - The email content and sender domain confirm a **phishing attempt (True Positive)**.  
   - Since no connection attempts were observed, **no escalation** was necessary.  

---

## 🧾 Case Report Summary

| Field | Entry |
|-------|-------|
| **Time of Activity** | 2025-10-22 10:36:32 UTC |
| **Affected Entity** | h.harris@thetrydaily.thm |
| **Incident Type** | Phishing Email |
| **Classification** | True Positive |
| **Escalation Required** | No |
| **Indicators of Compromise (IOCs)** | `urgents@amazon.biz`, `bit.ly/3sHkX3da12340` |
| **Recommended Actions** | Quarantine email, block sender domain, user awareness reminder |

---

## 🧰 Skills Practiced
- SIEM investigation using Splunk  
- Phishing triage and URL analysis  
- IOC extraction and validation  
- True/False positive classification  
- Incident documentation and communication  

---

## 💡 Reflection
This lab strengthened my understanding of SOC workflows — from alert validation to incident documentation.  
It reinforced when escalation is appropriate and how to provide concise, actionable recommendations in a case report.

----

*Note: This write-up summarizes personal learning from a public TryHackMe lab.  
No proprietary data or full solutions are shared.*

