# VMWare Horizon Parser

## Description
This parser extracts and normalizes **VMware Horizon syslog events** from the `Syslog` table in Microsoft Sentinel.  
It helps identify user logins, logoffs, authentication failures, SSO credential locks, licensing updates, and other Horizon-related events.  

Key points:
- Extracts **user activity** (login, logout, failed authentication).  
- Captures **requests** (desktop launches, XML API requests).  
- Provides structured fields for **security monitoring and troubleshooting**.  
- Enables detection of abnormal access behavior in Horizon environments.  

## Log Source
- **Table:** Syslog  
- **Device/Product:** VMware Horizon (via Horizon Connection Server syslogs)  
- **Filter:** `Computer == "PlaceHereTheVMhorizonHostORHosts"` (update with your Horizon host(s))  

## Notes
- Replace `"PlaceHereTheVMhorizonHostORHosts"` with your actual **VM Horizon Connection Server host(s)**.  
- The parser covers **common authentication and system events**, but can be extended to capture more fields if needed.  
- Recommended for SOC teams monitoring **user access patterns, failed logins, and potential misuse** of Horizon environments.  
