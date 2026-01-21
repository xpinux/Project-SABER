## HoaxShell Command-and-Control via PowerShell or CMD

## Description

This detection identifies execution patterns associated with **HoaxShell**, a lightweight command-and-control (C2) framework that abuses **PowerShell** or **CMD** for remote command execution over HTTP.

HoaxShell commonly leverages:
- Inline environment variable manipulation
- Repeated `curl` requests
- Custom `Authorization` headers
- Infinite or looping execution logic
- Temporary script creation and execution

This behavior is indicative of **active C2 communication** and post-exploitation activity.

## Log Source

- **Table:** DeviceProcessEvents  

## Detection Logic

The rule detects:

- Execution of `powershell.exe` or `cmd.exe`
- Command lines containing:
  - Embedded `Authorization` headers
  - HTTP-based `curl` requests
  - Looping execution logic
  - Temporary batch file creation and execution

These patterns closely align with known **HoaxShell tradecraft**.

## Configuration

- Recommended query scheduling frequency: 5 minutes
- Recommended lookup period: 15 minutes
- Severity Recommendation: High

## Entity Mapping

`HostName`

`InitiatingProcessAccountName`

`FileName`

`InitiatingProcessCommandLine`

## MITRE ATT&CK Mapping

- T1059.001 – Command and Scripting Interpreter: PowerShell

- T1059.003 – Command and Scripting Interpreter: Windows Command Shell

- T1071.001 – Application Layer Protocol: Web Protocols

- T1105 – Ingress Tool Transfer

## Recommendations / Tuning

This detection is high-fidelity and false positives are unlikely.
However, consider exclusions if:

Internal red team or penetration testing activity is ongoing

Authorized security tooling mimics similar C2 patterns
