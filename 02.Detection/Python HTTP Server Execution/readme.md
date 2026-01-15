## Python HTTP Server Execution

## Description

This detection identifies instances where **Python is used to start a built-in HTTP server** via the `-m http.server` module.

Attackers commonly abuse Python’s lightweight HTTP server for:
- Data exfiltration
- Payload hosting
- Local file transfer
- Lateral movement staging
- Ad-hoc C2 or callback infrastructure in restricted environments

Because this capability is built into Python and does not require additional tooling, it is frequently observed in post-exploitation activity and red-team operations.

## Data Source

### Table
- `DeviceProcessEvents`

## Detection Logic

The rule detects execution of Python interpreters (`python.exe` or `python3.exe`) where the command line contains:

- `-m http.server`

This module launches a simple HTTP server on a specified or default port (typically 8000).

Both **direct execution** and **execution via a parent process** are covered.

## Recommended Rule Configuration

- **Query frequency:** 5 minutes  
- **Lookup period:** 30 minutes  
- **Recommended severity:** Medium  

## Entity Mapping

### HostName
- `DeviceName`

### AccountName
- `InitiatingProcessAccountName`

### Process
- `FileName`
- `ProcessCommandLine`

## MITRE ATT&CK Mapping

### Primary Techniques
- **T1059.006 – Command and Scripting Interpreter: Python**

## Known False Positives

- Developers running local test servers
- CI/CD pipelines
- Training labs
- Python tutorials or documentation examples
