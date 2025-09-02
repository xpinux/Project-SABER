# Server-WindowsFirewall Changes

## Description
This detection identifies attempts to **disable or modify Windows Firewall settings** using PowerShell or command-line utilities.  
It monitors for commands that:
- Copy files and modify firewall rules (`Copy-Item` + `netsh firewall add rule`)  
- Disable current firewall profiles (`netsh advfirewall set currentprofile state off`)  
- Change firewall operation mode (`netsh firewall set opmode mode=disable`)  
- Enable new firewall rules or manipulate rule groups (`netsh firewall set rule group=... enable=Yes`)  
- Modify firewall policy registry keys (`New-ItemProperty HKLM:\SOFTWARE\POLICIES\Microsoft\WindowsFirewall`)  

These actions are commonly observed during **post-compromise activities**, lateral movement, or attempts to bypass endpoint security controls.

## Log Source
- **Table:** SecurityEvent  
- **Field:** CommandLine  

## Configuration
- **Recommended query scheduling frequency:** 1 hour  
- **Recommended lookup period:** 1 hour  
- **Severity Recommendation:** Medium  

## Entity Mapping
- AccountName  
- Computer  
- CommandLine  

## MITRE ATT&CK Mapping
- **T1562 – Impair Defenses**  
- **T1089 – Disabling Security Tools**  

## Recommendations
- Simulate results in Sentinel before enabling to check for false positives.  
- Exclude legitimate administrative scripts if they manage firewall configurations regularly.  
- Monitor triggered alerts immediately, as this usually indicates **potential malicious activity**.
