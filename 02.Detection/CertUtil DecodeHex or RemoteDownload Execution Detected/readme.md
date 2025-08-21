# **Detection: Certutil DecodeHex Usage**

## **Description**
This KQL detection identifies suspicious use of **certutil.exe** with the `-decodehex` flag, which can indicate attempts to decode a hex-encoded file — a technique often associated with **malware obfuscation** or **data exfiltration**.  

Adversaries may also misuse **certutil** to transfer tools or files from external systems into a compromised environment. Such activity leverages this living-off-the-land binary (LOLBIN) to download or decode malicious content without relying on external utilities.  

---

## **Log Source**
- **Table:** `DeviceProcessEvents`  
- **Process:** `certutil.exe`  

---
