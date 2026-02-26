# Accessibility Features Binaries Tampering

## Description

This detection identifies **potential tampering of Windows accessibility binaries**, a well-known persistence and logon bypass technique abused by attackers.  
Windows accessibility executables such as `sethc.exe` and `utilman.exe` can be replaced or modified to execute arbitrary commands **before authentication**, allowing attackers to gain SYSTEM-level access from the logon screen.

This rule monitors file creation, modification, or renaming events involving accessibility binaries while **excluding known legitimate system processes** such as Windows Update and TrustedInstaller.

## Log Source

- **Table:** DeviceFileEvents  
 
## Configuration

- Recommended query scheduling frequency: 15 minutes
- Recommended lookup period: 15 minutes
- Recommended Severity: Medium

## MITRE ATT&CK Mapping

This detection aligns with the following MITRE ATT&CK techniques:

- T1546.008 – Event Triggered Execution: Accessibility Features
- T1547 – Boot or Logon Autostart Execution
  
## Recommendations / Tuning

When this alert fires:

- Verify whether the file hash matches the legitimate Windows binary
- Check if the binary has been replaced with cmd.exe or powershell.exe
- Identify the user and process responsible for the modification
- Inspect for additional persistence mechanisms

Correlate with:

- DeviceProcessEvents
- DeviceLogonEvents
- Registry modifications related to logon behavior
