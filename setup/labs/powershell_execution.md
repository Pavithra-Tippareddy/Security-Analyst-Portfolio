# Lab: PowerShell Execution Visibility (Event IDs 4103 & 4104)

## Objective
Enable and verify PowerShell Module Logging (4103) and Script Block Logging (4104). Produce test PowerShell activity and confirm logs appear in Event Viewer and in Splunk.


## Why
ScriptBlock & Module logging give visibility into PowerShell usage — helpful to detect attackers using encoded, obfuscated, or living-off-the-land PowerShell commands.


## Setup (enable logging — use Administrator)

> **Option A — Registry (works on Home / no gpedit):**
Run an elevated PowerShell or Command Prompt and paste these (one line each):

```powershell
reg add "HKLM\SOFTWARE\Policies\Microsoft\Windows\PowerShell\ScriptBlockLogging" /v EnableScriptBlockLogging /t REG_DWORD /d 1 /f
reg add "HKLM\SOFTWARE\Policies\Microsoft\Windows\PowerShell\ModuleLogging" /v EnableModuleLogging /t REG_DWORD /d 1 /f
reg add "HKLM\SOFTWARE\Policies\Microsoft\Windows\PowerShell\ModuleLogging\ModuleNames" /v "*" /t REG_SZ /d "*" /f

* After running the above: either run gpupdate /force (may be limited on Home) or reboot the machine.

## Option B — regedit GUI
* If you prefer GUI: open regedit (Run → regedit) as admin and create the same keys/values:

* HKLM\SOFTWARE\Policies\Microsoft\Windows\PowerShell\ScriptBlockLogging\EnableScriptBlockLogging = DWORD 1
* HKLM\SOFTWARE\Policies\Microsoft\Windows\PowerShell\ModuleLogging\EnableModuleLogging = DWORD 1
* HKLM\SOFTWARE\Policies\Microsoft\Windows\PowerShell\ModuleLogging\ModuleNames\* = REG_SZ "*"

## Test commands (generate logs)
1. Open PowerShell (as normal user) (don’t need admin for these test commands):
   * Get-Process
   * Get-Service
   * Write-Output "PS Test: basic commands"

## Verify in Event Viewer.
* Open Event Viewer → Applications and Services Logs → Microsoft → Windows → PowerShell → Operational
* Look for Event ID 4103 (Module logging / pipeline) — shows commands as they execute.
* Look for Event ID 4104 (Script block logging) — shows the full script text or script block.

## Splunk Searches (SPL)

# Basic 4103/4104 search:

* index=wineventlog (EventCode=4103 OR  EventCode=4104)
| table _time host Account_Name EventCode ScriptBlockText Message
| sort - _time

** Expected results:
# Get-Process / Get-Service show up as 4103 entries describing module/pipeline calls.
# Splunk searches should return those events when the correct index/sourcetype is used.

## Troubleshooting

## If you see 4104 but not 4103: ModuleLogging not fully configured — re-run the ModuleLogging registry command or ensure ModuleNames\* exists.

* If nothing appears: confirm Event Viewer path Applications and Services Logs → Microsoft → Windows → PowerShell → Operational shows events (if not, reboot).

* In Splunk: verify you indexed Microsoft-Windows-PowerShell/Operational and that your index= in SPL matches the index configured.

## Screenshots under - screenshots/powershell/.gitkeep




