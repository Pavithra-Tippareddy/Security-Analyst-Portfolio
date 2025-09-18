# Windows Logging Setup (Lab Practice)

## 🎯 Goal
Enable logging for Security events (logons) and PowerShell Script Block logging so they can be analyzed in Splunk.


## 1. Security Event Logging
We used built-in auditing (already enabled in Windows) to capture logon attempts.

✅ Relevant Event IDs:
- **4624** = Successful login
- **4625** = Failed login


## 2. PowerShell Script Block Logging
Since gpedit.msc is not available in Windows Home, we enabled logging using **Registry Editor**.

Steps:
1. Open `regedit`.
2. Navigate to:  
   `HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows`
3. Create a new key: **PowerShell**  
   Under it, create another key: **ScriptBlockLogging**
4. Inside `ScriptBlockLogging`, create a **DWORD (32-bit) Value**:
   - Name: `EnableScriptBlockLogging`  
   - Value: `1`
5. Restart the machine or run a test command.

✅ Relevant Event ID:
- **4104** = Script block execution (we tested with `Write-Output "Hello Pavithra"` and saw logs).

-
## 3. Verification
- Open **Event Viewer** → Applications and Services Logs → Microsoft → Windows → PowerShell → Operational.
- We confirmed:
  - **4625** appeared when entering wrong password using `runas`.
  - **4104** appeared when running `Write-Output "Hello Pavithra"`.


## 4. Splunk
- Added **PowerShell/Operational** log source manually into Splunk’s `inputs.conf`.
- Verified events (4625, 4624, 4104) by running Splunk queries:

  index=wineventlog EventCode=4625
  index=wineventlog EventCode=4624
  index=wineventlog EventCode=4104

✅ Summary

** We successfully enabled:

# Logon event logging (4624/4625).
# PowerShell Script Block logging (4104).
# Both were ingested into Splunk and confirmed with test events.

