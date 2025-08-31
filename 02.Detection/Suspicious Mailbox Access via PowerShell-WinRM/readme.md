# Suspicious Mailbox Access via PowerShell/WinRM

## Description
This detection identifies potential misuse of **PowerShell** or **WinRM** to access mailboxes.  
Such activity may indicate suspicious behavior, including:
- Attackers using remote administration tools to access email accounts.  
- Attempts to bypass traditional email clients or browser logins.  
- Possible lateral movement, credential theft, or privilege abuse.  

## Log Source
- **Table:** OfficeActivity  
- **Operation:** MailboxLogin  

## Configuration
- **Recommended query scheduling frequency:** 1 hour  
- **Recommended lookup period:** 24 hours  
- **Severity Recommendation:** Medium-High  

## Entity Mapping
- UserAgent  
- UserId  
- MailboxId  

## MITRE ATT&CK Mapping
- **T1078 – Valid Accounts**  
- **T1086 – PowerShell**  

## Recommendations / Tuning
- Consider **excluding known service accounts or automation accounts** to reduce false positives.  
- Adjust the query to include additional suspicious user agents if your environment uses custom scripts.  
