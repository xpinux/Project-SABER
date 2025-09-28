# Network Capture Tools Usage

## Description  
This detection identifies the execution of known **packet capture and sniffing tools** (e.g., Wireshark’s `tshark.exe`, `tcpdump`, `ettercap`, `bettercap`).  
Attackers may deploy these utilities to capture sensitive traffic, extract credentials, or monitor network activity.  
The rule also inspects **command-line arguments** commonly used for capturing raw traffic, disabling promiscuous mode protections, or writing capture files to disk.  

**Key points:**  
- Detects usage of well-known capture binaries (`tshark.exe`, `tcpdump`, `ettercap`, etc.).  
- Flags suspicious command-line arguments (`-I`, `--monitor-mode`, `-w`, `-i`, etc.).  
- Summarizes detections with first/last seen timestamps, number of hits, and up to 5 unique command-line samples for quick triage.  

## Log Source  
- **Table:** `DeviceProcessEvents`  
- **FileName:** Packet capture tools (tshark.exe, tcpdump.exe, windump.exe, ettercap, bettercap, etc.)  

## Configuration  
- **Lookback period:** 1 hour (configurable via parameter)  
- **Recommended query scheduling frequency:** 1 hour  
- **Recommended lookup period:** 1 hour 
- **Severity Recommendation:** High  

## Entity Mapping  
- **HostName** → `DeviceName`  
- **Account** → `InitiatingProcessAccountUpn`, `AccountName`  
- **FileName** → `FileName`  
- **CommandLine** → `Samples`  

## MITRE ATT&CK Mapping  
- **T1040 – Network Sniffing**  

