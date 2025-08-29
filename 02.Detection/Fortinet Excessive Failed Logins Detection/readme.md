# Fortinet Excessive Failed Logins Detection

## Description
This detection identifies potential **brute-force** or **credential stuffing** activity targeting Fortinet devices.  

It analyzes failed login attempts captured in the **CommonSecurityLog** table and raises an alert if:
- More than **400 failed login attempts** from a single computer with the same message occur, or  
- The **total number of failed login attempts** across all records exceeds **200** in the queried period.  

This rule helps surface excessive authentication failures which may indicate **malicious activity** or **misconfigured systems**.  

## Log Source
- **Table:** CommonSecurityLog  
- **Vendor:** Fortinet  
- **Product:** Fortinet Devices  

## Configuration
- **Recommended query scheduling frequency:** 1 hour  
- **Recommended lookup period:** 1 hour  
- **Severity Recommendation:** High  

## Entity Mapping
- AccountName (if available in Message field)  
- Computer  

## MITRE ATT&CK Mapping
- **T1110 – Brute Force**  
