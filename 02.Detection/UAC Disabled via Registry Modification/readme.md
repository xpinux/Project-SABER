# Detection Rule — UAC Disabled via Registry Modification

## Description  
This detection identifies when User Account Control (UAC) is disabled on Windows endpoints by setting the registry value `EnableLUA` to `0`.  
Attackers and malware often modify this registry key to weaken local security controls, bypass privilege escalation prompts, and operate with fewer restrictions.  

**Key points:**  
- Tracks registry modifications under:  
  `HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System`  
- Flags when `EnableLUA` is explicitly set to `0`.  
- Helps detect attempts to weaken endpoint hardening and elevate privileges silently.  

## Log Source  
- **Table:** `DeviceRegistryEvents`  
- **ActionType:** `RegistryValueSet`  
- **RegistryKey:** `\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System`  
- **RegistryValueName:** `EnableLUA`  

## Configuration  
- **Recommended query scheduling frequency:** 1 hour  
- **Recommended lookup period:** 1 day  
- **Severity Recommendation:** High  

## Entity Mapping  
- **Host** → `DeviceName`  
- **Account** → `InitiatingProcessAccountName`  
- **Process** → `InitiatingProcessFileName`
- **RegistryValueName** → `RegistryValueName`  

## MITRE ATT&CK Mapping  
- **T1548.002 – Abuse Elevation Control Mechanism: Bypass User Access Control**
