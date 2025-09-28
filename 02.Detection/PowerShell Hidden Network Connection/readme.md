# PowerShell Hidden Network Connection

## Description
This detection identifies instances where **PowerShell is launched with hidden window styles** and establishes **outbound network connections**.  
Attackers often use `-WindowStyle Hidden` or similar arguments to execute malicious scripts without user visibility.  
Combined with external network activity, this behavior can indicate **command-and-control (C2)**, **data exfiltration**, or **malware execution**.

Key points:
- Detects **PowerShell.exe** and **Pwsh.exe** processes
- Flags **hidden execution mode**
- Filters out private IPs to focus on **external connections**
- Provides context: command line, account, remote IP/URL

---

## Log Source
- **Table:** `DeviceNetworkEvents`
- **Process:** `powershell.exe` / `pwsh.exe`

---

## Configuration
- **Recommended query scheduling frequency:** 1 hour
- **Recommended lookup period:** 1 hour
- **Severity Recommendation:** High

---

## Entity Mapping
- `DeviceName`
- `InitiatingProcessAccountName`
- `InitiatingProcessCommandLine`
- `RemoteIP`
- `RemoteUrl`

---

## MITRE ATT&CK Mapping
- **T1059.001 – Command and Scripting Interpreter: PowerShell**  
- **T1071 – Application Layer Protocol (C2 communication)**  
