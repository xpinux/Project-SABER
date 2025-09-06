# iDRAC Parser

## Description
This parser extracts and normalizes **Dell iDRAC (Integrated Dell Remote Access Controller)** syslog events from the `Syslog` table in Microsoft Sentinel.  
It provides structured fields for device name, severity, category, message ID, and detailed message content, making it easier to monitor server health, hardware alerts, and remote access activity.

## Log Source
- **Table:** Syslog  
- **Device:** Dell iDRAC  

## Extracted Fields
- `DeviceName` – iDRAC device name (e.g., `iDRAC-Server01`)  
- `Severity` – Event severity level  
- `Category` – Event category (hardware, firmware, security, etc.)  
- `MessageID` – Unique identifier for the event type  
- `Message` – Detailed description of the event   

## Notes
- The default filter uses `SyslogMessage contains "iDrac"`.  
  - If you want to target a specific server system, replace with:  
    ```kql
    | where Computer contains "<ServerNameOrIP>"
    ```
- Useful for detecting critical hardware events, failed login attempts, and remote access operations.
