# Suspicious PowerShell Downgrade to Version 2

## Description

This detection identifies the execution of **PowerShell Version 2**, an outdated and insecure version of PowerShell that lacks many modern security features such as Script Block Logging, AMSI integration, and enhanced event logging.

Attackers often intentionally invoke PowerShell v2 to **bypass security controls**, evade logging, and execute malicious scripts with reduced visibility. Any execution of PowerShell v2 in modern environments should be treated as **highly suspicious**, unless explicitly justified.

## Log Source

- **Table:** DeviceProcessEvents  

## Detection Logic

The rule detects:
- Explicit execution of PowerShell binaries (`powershell.exe`, `powershell_ise.exe`)
- Command lines containing `version 2`, which forces PowerShell to run using v2 syntax and engine

This behavior is uncommon in legitimate use cases and strongly associated with **defense evasion techniques**.

## Configuration

- Recommended query scheduling frequency: 15 minutes
- Recommended lookup period: 1 hour
- Severity Recommendation: Medium

## Entity Mapping

- HostName
- ProcessCommandLine
- AccountName

## MITRE ATT&CK Mapping

- T1059.001 – Command and Scripting Interpreter: PowerShell
- T1562.001 – Impair Defenses: Disable or Modify Security Tools

## Recommendations / Tuning

PowerShell Version 2 should be disabled entirely in modern environments.
