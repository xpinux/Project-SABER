# EventLogs Cleared with Wevtutil

## Description
This detection identifies suspicious attempts to **clear Windows Event Logs** using the built-in utility **wevtutil.exe** or related PowerShell commands.  
Adversaries often clear logs to **erase evidence of their activity**, hinder **incident response**, and complicate **forensic investigations**.  

Indicators include usage of:
- `wevtutil cl`  
- `wevtutil.exe cl`  
- `Clear-EventLog` (PowerShell)  
- Other suspicious log-clearing command variations  

## Log Source
- **Table:** SecurityEvent  
- **Process:** wevtutil.exe / PowerShell  

## Configuration
- **Recommended query scheduling frequency:** 1 hour  
- **Recommended lookup period:** 1 hour  
- **Severity Recommendation:** High  

## Entity Mapping
- AccountName  
- DeviceName  
- ProcessCommandLine  

## MITRE ATT&CK Mapping
- **T1070.001 – Indicator Removal on Host: Clear Windows Event Logs**  
