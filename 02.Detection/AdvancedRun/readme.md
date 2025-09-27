# AdvancedRun Execution

## Description  
This detection identifies the execution of **AdvancedRun.exe**, a NirSoft utility that allows users (and attackers) to launch processes with custom privileges, environment variables, and other advanced parameters.  
Adversaries may leverage this tool to bypass normal execution restrictions, escalate privileges, or maintain persistence.  

**Key points:**  
- Detects direct execution of `AdvancedRun.exe`.  
- Provides visibility into process lineage and parent process.  
- Useful for spotting unauthorized or suspicious administrative activity.  

## Log Source  
- **Table:** `DeviceProcessEvents`  
- **FileName:** `AdvancedRun.exe`  

## Configuration  
- **Recommended query scheduling frequency:** 1 hour  
- **Recommended lookup period:** 1 day or 1 hour  
- **Severity Recommendation:** Medium to High (depending on environment and usage policy)  

## Entity Mapping  
- **Host** → `DeviceName`  
- **Account** → `InitiatingProcessAccountName`  
- **FileName** → `FileName`  
- **Hash** → `InitiatingProcessSHA1`  

## MITRE ATT&CK Mapping  
- **T1548 – Abuse Elevation Control Mechanisms**  
