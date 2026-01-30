# Advanced IP Scanner Execution

## Description

This detection identifies the execution of **Advanced IP Scanner** and similar GUI-based network scanning tools on endpoints.  
Such tools are commonly used for **network discovery and reconnaissance** and may indicate **unauthorized internal scanning**, especially when executed by non-IT users or on high-value assets.

While Advanced IP Scanner can be used legitimately by administrators, attackers and red teams frequently leverage it for **rapid host enumeration** during post-compromise activity.

## Log Source

- **Table:** DeviceProcessEvents  

## Detection Logic

The rule monitors endpoint process creation events and flags executions of known **Advanced IP Scanner binary name variants**, including common renamed or repackaged versions.

It aggregates activity over a configurable lookback window to provide:
- First and last execution timestamps
- Execution count
- Sample command-line usage

## Configuration

- Recommended query scheduling frequency: 1 hour
- Recommended lookup period: 1 hour
- Severity Recommendation: Low
  
## MITRE ATT&CK Mapping

- T1046 – Network Service Discovery

## Investigation Guidance

When this detection triggers:

- Identify the user executing the scanner
- Validate whether the activity aligns with approved IT operations

## Tuning & False Positives

- IT inventory or troubleshooting
- Network mapping during maintenance
- Authorized penetration testing
