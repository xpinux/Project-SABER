# Multiple Account Lockouts in Short Timeframe

## Description
This detection identifies **multiple user account lockouts (Event ID 4740) within a 10-minute window**.  
A high volume of lockouts across different accounts in a short timeframe is a common indicator of **password spraying attacks**, brute-force attempts, or widespread misconfigurations.

## Key Points
- Monitors for **Event ID 4740** (Account Lockout).  
- Groups by **host (Computer)** and **time bin (10m)**.  
- Flags when **more than 10 unique accounts** are locked out in the defined timeframe.  
- Provides a list of affected users and potential caller sources.  

---

## Log Source
- **Table:** `SecurityEvent`  
- **Event ID:** `4740` (Account Lockout)

---

## Configuration
- Recommended query scheduling frequency: 10 minutes
- Recommended lookup period: 10 minutes
- Severity Recommendation: High
  
---

## Entity Mapping
- HostName: Computer
- AccountName: AccoutName

---

 # MITRE ATT&CK Mapping
- T1110.003 – Brute Force: Password Spraying
- T1499 – Account Lockout / Service Disruption (impact if accounts are disabled)
  
---

# Recommendations / Tuning
- Adjust threshold: Modify UniqueUsers > 10 to match your environment size and normal activity.
- Exclude known service accounts: Add common accounts that frequently lock out due to misconfigured applications.
- Baseline normal lockouts: Compare against typical lockout rates per host/domain.
- Investigate Sources field: Identify the machine or service responsible for the lockouts.
