# Credential Dumping - Suspicious Process -comsvcs

## Description
This detection identifies suspicious use of **rundll32.exe** to invoke **comsvcs.dll**, a technique often used in **credential dumping attacks**.  
Adversaries may leverage this method to access and extract sensitive credentials from memory or the LSASS process without deploying additional binaries, allowing stealthy credential theft.  

Key points:
- Detects execution of `rundll32.exe` with parameters targeting `comsvcs.dll`.  
- Monitors multiple relevant Windows events, including:
  - **EventID 1** – Security event (generic process creation)  
  - **EventID 4688** – New process creation  
  - **EventID 4104** – PowerShell script block logging (if rundll32 is invoked via PowerShell)  

## Log Source
- **Table:** SecurityEvent  
- **EventID:** 1, 4688, 4104  
- **Process:** rundll32.exe  

## Configuration
- **Recommended query scheduling frequency:** 1 hour  
- **Recommended lookup period:** 1 hour  
- **Severity Recommendation:** Medium  

## Entity Mapping
- AccountName  
- Computer  
- ProcessCommandLine  
- ParentProcessName  

## MITRE ATT&CK Mapping
- **T1003.006 – OS Credential Dumping: LSASS Memory**  

## Recommendations / Tuning
- Exclude known administrative scripts or maintenance tasks that legitimately use `rundll32.exe comsvcs.dll`.  
- Consider monitoring only unusual or unexpected hosts/accounts to reduce false positives.  
