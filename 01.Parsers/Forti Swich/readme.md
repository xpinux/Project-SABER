# FortiSwitch Parser

## Description
This parser extracts and normalizes **Forti Switch syslog events** from the `Syslog` table in Microsoft Sentinel.  
It parses key FortiSwitch fields such as device ID, device name, user, action, port, status, and message details.  

Key points:
- Extracts structured fields for better analysis, threat detection, and investigation.  
- Supports tracking of network actions, switch port usage, and user activity.  
- Helps SOC analysts quickly identify configuration changes, security events, and network anomalies.

## Log Source
- **Table:** Syslog  
- **Device Vendor:** Fortinet  
- **Device Product:** FortiSwitch  
- **Message Filter:** `SyslogMessage contains "device_id="` (can be customized per device or DeviceID prefix)

## Notes
- Adjust the `SyslogMessage contains "device_id="` filter to match your FortiSwitch device IDs.  
- The parser captures key operational and security fields, which can be extended for advanced correlation and alerting.  
- Recommended for SOC teams monitoring FortiSwitch devices for network and security visibility.
