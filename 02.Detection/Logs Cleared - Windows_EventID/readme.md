# Logs Cleared - Windows

## Description
This detection identifies events where **Windows Event Logs have been cleared**.  
It leverages the built-in **SecurityEvent ID 1102**, which is generated whenever the event log is cleared.  
Clearing event logs is a common **log evasion technique** used by attackers to remove evidence of malicious activity.  

## Log Source
- **Table:** SecurityEvent  
- **EventID:** 1102  

## Configuration
- **Recommended query scheduling frequency:** 1 hour  
- **Recommended lookup period:** 1 hour  
- **Severity Recommendation:** High  

## Entity Mapping
- AccountName  
- DeviceName  

## MITRE ATT&CK Mapping
- **T1070.001 – Indicator Removal on Host: Clear Windows Event Logs**  

## False Positives / Tuning Guidance
Please ensure to **exclude service accounts or computers** that legitimately clear event logs for maintenance or operational purposes.  
Tuning the rule to ignore known maintenance accounts or scheduled log-clearing jobs will reduce false positives.

## Recommendations / Tuning

- Adjust filtering – if too noisy, focus on exact -WindowStyle Hidden instead of any hidden.
- Whitelist legitimate automation – exclude known scripts, update servers, or monitoring tools that use PowerShell silently.
- Expand visibility if needed – remove the private IP filter if attackers may operate internally.

