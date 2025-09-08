# Rundll32 COMSVCS Execution Detection

## Description
This detection identifies suspicious use of **rundll32.exe** loading **comsvcs.dll**, which is commonly abused by attackers for credential dumping or executing malicious payloads.  
`rundll32.exe` is a trusted Windows binary (LOLBIN), but when paired with `comsvcs.dll`, it often indicates attempts to extract sensitive information from memory, such as credentials, or to evade defenses.

Key points:
- Monitors process creation logs where **rundll32.exe** is executed with **comsvcs.dll**.  
- Detects execution attempts via process creation (4688), script execution (4104), or Sysmon process creation (Event ID 1).  
- Helps surface suspicious use of native Windows binaries for malicious purposes.

## Log Source
- **Table:** SecurityEvent  
- **Event IDs:** 1, 4688, 4104  

## Configuration
- **Recommended query scheduling frequency:** 1 hour  
- **Recommended lookup period:** 1 hour  
- **Severity Recommendation:** Medium  

## Entity Mapping
- **Account:** `Account`  
- **Host:** `Computer`  
- **Process:** `CommandLine`  

## MITRE ATT&CK Mapping
- **T1003.001 – OS Credential Dumping: LSASS Memory**

## Recommendations / Tuning
- Review legitimate administrative uses of **rundll32.exe** with `comsvcs.dll`.  
- Whitelist trusted applications or automation scripts if necessary.  
- Consider correlating with other suspicious activity (e.g., LSASS access, credential dumping alerts).  
- Run **Simulate results** in Sentinel before enabling to check baseline noise levels.
