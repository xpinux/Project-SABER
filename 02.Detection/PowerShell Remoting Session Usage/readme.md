## PowerShell Remoting Session Usage (PSSession Invocation)

## Description

This detection identifies the use of **PowerShell Remoting** via interactive or non-interactive PSSession commands, including:

- `New-PSSession`
- `Enter-PSSession`
- `Invoke-Command -Session`

PowerShell Remoting leverages **WinRM** and is commonly abused by attackers for **lateral movement**, **remote command execution**, and **post-exploitation activities**, especially in Active Directory environments.

While PowerShell Remoting can be legitimate for administration, its usage should be tightly controlled and monitored.

## Data Source

- **Table:** `DeviceProcessEvents`

## Query Logic Summary

- Monitors PowerShell (`powershell.exe`, `pwsh.exe`) executions
- Detects PSSession-related remoting commands

## Recommended Rule Configuration

- **Query frequency:** 15 minutes  
- **Lookup period:** 1 hour  
- **Recommended severity:** Medium to High  

**Severity guidance:**
- Medium if PowerShell remoting is common in your environment
- High if used outside of approved admin hosts or by non-admin users

## Entity Mapping

Configure the following entity mappings in Microsoft Sentinel:

### HostName
- `DeviceName`
### AccountName
- `InitiatingProcessAccountName`
### Process
- `InitiatingProcessFileName`
- `CommandLine`

## MITRE ATT&CK Mapping

- **T1021.006 – Remote Services: Windows Remote Management**
- **T1059.001 – Command and Scripting Interpreter: PowerShell**

## Recommendations / Tuning

### Expected Behavior (False Positives)

Legitimate activity may include:
- IT administrators using PowerShell Remoting
- Automation frameworks and orchestration tools
- Scheduled maintenance or deployment scripts

### Tuning Guidance

- Exclude:
  - Known administrative jump hosts
  - Service accounts used for automation
  - Approved scripts or repositories
- Enhance fidelity by:
  - Correlating with network logons (Type 3 / WinRM)
  - Alerting when used from workstations instead of servers
  - Raising severity when executed by non-admin users


