## Outbound Communication to Telegram API

## Description

This detection identifies **outbound network traffic to Telegram’s public API (`api.telegram.com`)** observed in perimeter or network security device logs.

Telegram is frequently abused by threat actors as:
- A **Command and Control (C2)** channel
- A **data exfiltration** endpoint
- A **drop zone for malware notifications**

While Telegram usage can be legitimate, **direct API communication from servers, network devices, or security zones where instant messaging is not expected** should be reviewed carefully.

## Data Source

### Table
- `CommonSecurityLog`

### Typical Devices
- Firewalls
- Web Proxies
- Secure Web Gateways
- Network IDS/IPS

## Detection Logic

The rule detects HTTP/S requests where the destination URL contains:

- `api.telegram.com`

This endpoint is used by:
- Telegram Bots
- Automation frameworks
- Malware families leveraging Telegram Bot APIs
