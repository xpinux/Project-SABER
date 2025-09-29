# Enumeration of Sensitive Groups via Command-Line Tools

## Description
This detection identifies attempts to enumerate **highly privileged Active Directory groups** such as:
- Domain Admins
- Enterprise Admins
- Administrators
- Schema Admins
- Account Operators
- Server Operators
- Backup Operators
- DnsAdmins
- Exchange Organization Administrators

Attackers often use built-in Windows tools (`net.exe`, `net1.exe`, `cmd.exe`, `PowerShell`, `pwsh.exe`, `adfind.exe`, `dsquery.exe`, `dsget.exe`, `wmic.exe`, `whoami.exe`) to perform **group enumeration**, which is a common precursor to privilege escalation or lateral movement.

## Log Source
- **Table:** DeviceProcessEvents

# Entity Mapping
- HostName: DeviceName
- AccountName: InitiatingProcessAccountName

# Recommended Query Settings
- Query Frequency: 1 hour
- Lookup Period: 1 hour

# Severity: High

# MITRE ATT&CK Mapping
- Tactic: Discovery
- Technique: T1069.002 — Permission Groups Discovery: Domain Groups

# Recommendations / Tuning

- Exclusions: Add known IT service or maintenance accounts to the ExcludedHosts array to reduce false positives.
- Localization: Adjust group names if your AD is not in English (e.g., Administratoren in German).
- Command Variations: Consider adding obfuscated PowerShell commands or alternative enumeration tools if used in your environment.
- Lookback Window: Increase or decrease the ago(1h) timeframe depending on normal administrative activity.
- Thresholds: Review Hits count to understand normal activity vs. potential malicious attempts.


