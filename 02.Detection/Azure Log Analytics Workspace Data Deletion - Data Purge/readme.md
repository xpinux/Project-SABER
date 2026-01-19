## Azure Log Analytics Workspace Data Deletion - Data Purge**

## Description

This detection identifies **successful attempts to delete data from an Azure Log Analytics workspace**.

Deleting data from a workspace can significantly impact:
- Incident response and forensics
- Compliance and audit requirements
- Detection and visibility coverage

While data deletion can be legitimate (e.g., GDPR requests, cost management), it is also a **high-risk administrative action** and may indicate:
- Defense evasion
- Log tampering
- Malicious insider activity
- Post-compromise cleanup by an attacker

This rule focuses only on **accepted (successful)** deletion operations.

## Data Source

### Table
- `AzureActivity`

## Detection Logic

The rule detects Azure Activity operations related to data deletion in Log Analytics workspaces, including:

- `Delete specified data from workspace`
- Operations containing `Delete Data`
- Operations containing `DeleteData`
- Common misspelling variants (e.g. `DeletaData`)

Only events with `ActivityStatus == "Accepted"` are included to reduce noise from failed attempts.

## Recommended Rule Configuration

- **Query frequency:** 5 minutes  
- **Lookup period:** 1 hour  
- **Recommended severity:** High  

## Entity Mapping

### Account

## MITRE ATT&CK Mapping

### Primary Technique
- **T1562.002 – Impair Defenses: Disable or Modify Cloud Logs**

## Known False Positives

- GDPR or privacy-related data deletion requests
- Approved data retention or cost-reduction activities
- Automated cleanup jobs executed by platform administrators
