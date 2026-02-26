# Windows IIS Password Recovery via AppCmd

## Description

This detection identifies **potential credential recovery or credential harvesting activity** against **Microsoft IIS application pools** using the built-in `appcmd.exe` utility.

Attackers may abuse `appcmd.exe` to enumerate IIS configuration and extract **clear-text or reversible credentials** associated with application pools, specifically the `processModel.username` and `processModel.password` properties. This technique is commonly used during **post-compromise credential access** and **privilege escalation** phases.

Because `appcmd.exe` is a legitimate IIS administration tool, misuse can blend into normal administrative activity if not carefully monitored.

## Log Source

- **Table:** DeviceProcessEvents  

## Detection Logic

The rule triggers when:
- `appcmd.exe` is executed
- The command line includes listing or configuration actions
- Sensitive IIS application pool properties are queried, including:
  - `processModel.password`
  - `processModel.username`
  - `/section:applicationPools`
  - Generic `password` or `username` keywords

These combinations strongly indicate **credential discovery attempts** rather than routine IIS administration.

## Configuration

 - Reccomended Severity: Medium
 - Query scheduling frequency: 15 minutes
 - Lookup period: 15 minutes

## Entities 

- HostName: DeviceName
- Account: InitiatingProcessAccountName
- Process Command Line: CmdLine
- Parent Process: InitiatingProcessFileName

  ## MITRE ATT&CK Mapping

- T1552.001 – Unsecured Credentials: Credentials In Files
- T1003 – OS Credential Dumping (related technique via service credential extraction)

## False Positive Guidance & Tuning

Expected Legitimate Activity

- IIS administrators performing
- Application pool troubleshooting
- Configuration audits
- Migration or backup operations
  
 When this alert triggers:

- Identify which application pool credentials were accessed
- Determine whether credentials are shared across systems
- Rotate exposed credentials immediately
- Review subsequent logon and network activity
- Inspect IIS configuration files for unauthorized changes
- Correlate with:
DeviceLogonEvents
DeviceNetworkEvents
SecurityEvent (service logons)
