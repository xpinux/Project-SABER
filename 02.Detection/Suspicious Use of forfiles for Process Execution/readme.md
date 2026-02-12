# Suspicious Use of forfiles for Process Execution

## Description

This rule detects potentially malicious usage of the **`forfiles`** utility to execute or manipulate executable or script files.  
Attackers may abuse `forfiles` to **spawn new processes**, **execute payloads**, or **evade defensive controls**, as it is a legitimate Windows binary often overlooked by security monitoring.

This behavior has been observed in:
- Malware execution chains
- Living-off-the-Land (LotL) techniques
- Defense evasion and persistence mechanisms

## Use Case

**Use of `forfiles` to start a new process to evade defensive countermeasures**

Attackers leverage `forfiles` to iterate over files and conditionally execute binaries or scripts, bypassing simple command-line or parent-process detections.

## Log Source

- **Table:** SecurityEvent  

## Detection Logic

The rule looks for command lines where:
- `forfiles` is invoked
- The command references executable or script file types such as:
  - `.exe`
  - `.dll`
  - `.bat`
  - `.ps1`
  - `.doc / .docm`
  - `.xls / .xlsm`
  - `.msi`

This combination strongly suggests **execution or staging of payloads** rather than benign file enumeration.

## Configuration  
- **Recommended query scheduling frequency:** 1 hour  
- **Recommended lookup period:** 1 day or 1 hour  
- **Severity Recommendation:** Medium 

## Entity Mapping  
- **Host** → `DeviceName`  
- **Account** → `InitiatingProcessAccountName`  
- **FileName** → `FileName`  
- **Hash** → `InitiatingProcessSHA1`
- **CommandLine** → `CommandLine`  

## MITRE ATT&CK Mapping  
- T1059.003 – Command and Scripting Interpreter: Windows Command Shell
- T1218 – Signed Binary Proxy Execution
