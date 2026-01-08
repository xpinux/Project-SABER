# Security Policy Export via Secedit

## Description

This detection identifies suspicious usage of **secedit.exe** to **export local security policies** from Windows systems.

`secedit.exe` is a legitimate Windows utility used to configure and analyze security policies. However, adversaries may abuse it to **export security configuration data**, including:
- Password policies
- Account lockout policies
- User rights assignments
- Security options

Exporting security policies can help attackers:
- Understand enforcement levels
- Identify weak configurations
- Prepare privilege escalation or persistence techniques

This rule monitors execution of `secedit.exe` with **export-related parameters**, which is uncommon outside administrative or maintenance workflows.

## Detection Logic

The rule detects:
- Execution of `secedit.exe` (directly or as a parent process)
- Usage of common export flags such as:
  - `/export`
  - `/cfg`
  - `-export`
  - `-cfg`
- Presence of `SECURITYPOLICY` in the command line
- Aggregates repeated executions per device and user context

Basic exclusions are included to reduce noise from mis-typed or known benign usage patterns.

## Log Source

- **Table:** DeviceProcessEvents
## Configuration

- **Recommended query scheduling frequency:** 30 minutes  
- **Recommended lookup period:** 1 hour  
- **Severity Recommendation:** Medium  

## Entity Mapping

### Host
- `DeviceName`
### Account
- `InitiatingProcessAccountUpn`
- `AccountName`
### Process
- `FileName`
- `ProcessCommandLine`
- `InitiatingProcessFileName`
- `InitiatingProcessCommandLine`

## MITRE ATT&CK Mapping

- **T1082 – System Information Discovery**  
  Exporting local security policies reveals detailed system configuration and security posture.
  
## Recommendations / Tuning

### Exclusions (Strongly Recommended)

Exclude known legitimate usage such as:
- Configuration management systems
- Security baseline and hardening deployments
- Approved administrative scripts and maintenance tasks

Common exclusion candidates:
- Known administrative service accounts
- Configuration management hosts (e.g., SCCM, Intune tooling)
- Scheduled maintenance windows

