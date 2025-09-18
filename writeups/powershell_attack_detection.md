PowerShell Script Block Logging – Detection Writeup
🔎 Objective

Tested PowerShell Script Block Logging (Event ID 4104) to observe how executed scripts are captured in Windows Event Viewer.

🛠️ Lab Steps Performed:
1. Enabled Script Block Logging through Windows Event Logging.
   
2. Opened PowerShell and executed a simple command:
   Write-Output "Hello Pavithra"

3. Opened Event Viewer → Applications and Services Logs → Microsoft → Windows → PowerShell → Operational.
   
4. Verified that the script block text (Hello Pavithra) appeared under Event ID 4104.

## Detection Outcome

* Event ID 4104 was successfully triggered.

* The executed script content was fully captured in the log.

* Demonstrated that PowerShell Script Block Logging provides visibility into all script contents, even simple test commands.


