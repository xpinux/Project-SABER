# Brute Force Failed Attempts - 5Min

## Description
This detection identifies potential **brute-force login attempts** on Windows systems over a **5-minute window**.  
It leverages **SecurityEvent ID 4625 (failed logon attempts)** and highlights accounts experiencing multiple authentication failures in a short period, which may indicate **credential stuffing, password spraying, or targeted brute-force attacks**.  

Key points:
- Tracks failed login attempts grouped by computer, logon process, account type, and account names.  
- Flags activity when the number of failed attempts in a 5-minute window exceeds **50**.  
- Helps surface **rapid authentication failures** that may indicate malicious activity or compromised accounts.  

## Log Source
- **Table:** SecurityEvent  
- **EventID:** 4625  

## Configuration
- **Recommended query scheduling frequency:** 5 minutes  
- **Recommended lookup period:** 5 minutes  
- **Severity Recommendation:** High  

## Entity Mapping
- Computer  
- LogonProcessName  
- AccountType  
- TargetUserName  
- TargetAccount  
- SubjectAccount  
- SubjectUserName  

## MITRE ATT&CK Mapping
- **T1110 – Brute Force**  

## Recommendations / Tuning
- **Adjust timerange:** Increase the `ago()` time in the query if you want to capture attacks over longer periods.  
- **Adjust failure threshold:** Lower or increase the `failurescount > 50` threshold depending on environment login volume.  
- **Exclude hosts:** Add known service or maintenance hosts to the `ExcludedHosts` array to reduce false positives.  

