# **Detection: Certutil DecodeHex Usage**

## **Description**
This KQL detection identifies suspicious use of **certutil.exe**, a Windows living-off-the-land binary (LOLBIN), in scenarios often abused by adversaries:  

- **Decoding activity** – Usage of `-decode` or `-decodehex` flags may indicate attempts to decode encoded files, commonly seen in **malware obfuscation** and **data exfiltration**.  
- **Suspicious download activity** – Usage of `http`, `urlcache`, and `-f` in the command line can indicate attempts to **download malicious tools or payloads** from remote sources.  

These techniques allow adversaries to leverage built-in Windows utilities to bypass security controls, avoid detection, and establish persistence without introducing new binaries.  

---

## **Log Source**
- **Table:** `DeviceProcessEvents`  
- **Process:** `certutil.exe`  

---
## **Configuration**

- Recommended query scheduling frequency: 1 hour
- Recommended lookup period: 1 hour
- Severity Recommendation: Medium

---
## **Entity Mapping**
- AccountName
- DeviceName
- FileName
- ProcessCommandLine
- InitiatingProcessCommandLine

## **MITRE ATT&CK Mapping**
`T1140 – Deobfuscate/Decode Files or Information`
