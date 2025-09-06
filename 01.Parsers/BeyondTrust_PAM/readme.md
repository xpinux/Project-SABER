# BeyondTrust PAM Parser

## Description
This parser normalizes and extracts detailed fields from **BeyondTrust PAM (BeyondInsight)** syslog events.  
It allows analysts to easily query important fields such as user, event name, role, authentication type, and more, for improved detection and investigation.

The parser supports multiple BeyondTrust appliances/servers (configured by IP or ProcessName) and extracts key-value pairs from `SyslogMessage`.

## Log Source
- **Table:** Syslog  
- **ProcessName:** BeyondInsight  

## Notes
- Update the **Computer IPs** or `ProcessName` filter to match your BeyondTrust environment.  
- Ensure logs are being ingested into the **Syslog table**.  
- Validate parsing by running the query against recent data.  
