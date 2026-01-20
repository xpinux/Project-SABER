## Local Administrator Group Modification via Command Line

## Description

This detection identifies attempts to **add accounts to the local Administrators group** using command-line utilities such as `net.exe`, `net1.exe`, PowerShell, or other processes capable of modifying local group membership.

Adding users to the local Administrators group is a **high-risk action** commonly associated with:
- Privilege escalation
- Persistence mechanisms
- Lateral movement preparation
- Post-exploitation activity

Threat actors frequently abuse commands like:
This rule focuses on command-line evidence of such behavior.

## Data Source

### Table
- `DeviceProcessEvents`

### Required Telemetry
- Microsoft Defender for Endpoint (MDE)
- 
## Detection Logic

The rule looks for process executions where:
- The command line contains `localgroup admin`
- The command line contains `add`

These conditions indicate an attempt to add a user to a privileged local group.

## Configuration

- Recommended query scheduling frequency: 5 minutes
- Recommended lookup period: 30 minutes
- Severity Recommendation: High

## MITRE ATT&CK Mapping

- T1098 – Account Manipulation
- T1078 – Valid Accounts

## Recommendations / Tuning
- Exclude Known Administrative Accounts
- Exclude legitimate service or IT admin accounts to reduce false positives:
- Exclude systems where administrative changes are expected:


## Investigation Guidance

When this alert is triggered:
- Identify who executed the command
- Validate which account was added
- Confirm business justification
- Review recent authentication activity
- Check for additional persistence or privilege escalation attempts


