# Windows Recovery Environment (WinRE) Disabled

## Description

This detection identifies attempts to **disable the Windows Recovery Environment (WinRE)** using `reagentc`.  
Attackers may disable WinRE to **impair system recovery**, **hinder forensic analysis**, or **prevent remediation actions** after compromise.

Disabling WinRE is uncommon in normal user activity and should be treated as **potential defense evasion**, especially when executed outside of approved IT maintenance workflows.

## Log Source

- **Table:** DeviceProcessEvents  

## Detection Logic

The rule monitors process creation events where:
- `reagentc.exe` is executed directly, or
- `reagentc` is invoked via `powershell.exe` or `cmd.exe`
- The command line includes the `disable` argument

This behavior indicates an attempt to disable Windows Recovery features.

## Configuration

- Recommended query scheduling frequency: 30 minutes
- Recommended lookup period: 1 hour
- Severity Recommendation: High
  
## MITRE ATT&CK Mapping

- T1562.001 – Impair Defenses: Disable or Modify Tools
- T1070 – Indicator Removal on Host

## Investigation Guidance

When this alert fires, analysts should:

- Confirm whether the action was performed by authorized IT personnel
- Identify the parent process and execution context
- Review recent administrative activity on the device
- Check for additional defense evasion behaviors (e.g., disabling AV, tampering with logs)
