# Failed Login Detection (Windows Event Logs)

### Objective
To generate and analyze failed login attempts and capture the related Windows Event Logs.

### Steps Performed
1. Used `runas` with incorrect passwords to simulate failed login attempts.
2. Verified logs in **Windows Event Viewer** under:
   - Security → Event ID **4625**
   - Account failed logon attempts
3. Enabled PowerShell logging (Module + Script Block) for further visibility.
4. Captured screenshots of the logs and analysis.

### Evidence
Screenshots stored under:
`screenshots/failed_logins/`

### Key Learning
- Event ID **4625** = Failed login attempt  
- Event ID **4624** = Successful login attempt  
- Monitoring these events is a core SOC skill for detecting brute-force attacks.

