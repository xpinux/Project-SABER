# Password Reset on Privileged Admins

## Description
This detection identifies when a **privileged administrator account** in Azure AD / Entra ID has its password reset.  
Privileged roles are high-value targets, and unauthorized resets could indicate account takeover or malicious insider activity.

## Relevant Roles
The rule monitors the following highly sensitive roles:
- Global Administrator  
- Authentication Administrator  
- Privileged Role Administrator  
- Company Administrator  
- Security Administrator  

## Data Sources
- **AuditLogs** – Captures Azure AD password reset events  
- **IdentityInfo** – Provides role assignment context for accounts  

## Detection Logic
1. Look for **password reset events** in `AuditLogs`.  
2. Extract the `TargetUsername` from `TargetResources`.  
3. Join against `IdentityInfo` to map assigned roles.  
4. Filter only for accounts with **privileged roles**.  
5. Summarize by timestamp, user, role, and operation.  

## Entities
1. `AccountName` TargetUsername 

## MITRE ATT&CK Mapping
- **Tactic:** Credential Access (TA0006)  
- **Technique:** Modify Authentication Process (T1556)  

## Recommended Actions
- Investigate **who initiated the reset** and validate if it was legitimate.  
- Review **sign-in activity** of the affected account before and after reset.  
- Check for **MFA enforcement** on the reset operation.  
- If suspicious, trigger **incident response** and rotate credentials.  

## Severity
**High** – Privileged accounts are critical assets.
