# Cisco Switch Parser

## Description
This parser extracts and normalizes **Cisco Switch syslog events** from the `Syslog` table in Microsoft Sentinel.  
It captures key Cisco log types such as login attempts, system messages, interface changes, STP, IP events, authentication logs, and crypto messages.  

The parser provides normalized fields for severity, facility, message content, user, source, and port information, making Cisco Switch logs more usable for detection, hunting, and dashboards.

## Log Source
- **Table:** Syslog  
- **Device:** Cisco Switches (IOS/IOS-XE/NX-OS)  
- **Message Types:** `%SEC_LOGIN`, `%SYS`, `%LINK`, `%STP`, `%IFMGR`, `%IP`, `%LINEPROTO`, `%CDP`, `%AUTH`, `%CRYPTO`  

## Extracted Fields
- `facility` – Syslog facility extracted from message  
- `severity` – Syslog severity level  
- `msg` – Parsed event message  
- `user` – User associated with login/auth events  
- `Source` – Source of event (IP or interface)  
- `localport` – Local port involved in the event  

## Notes
- Excludes syslog messages with `"system"` to reduce noise.  
- Can be expanded to parse additional Cisco syslog codes if required.  
- It’s recommended to test the parser with real Cisco switch logs to validate field extraction.
