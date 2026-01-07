# Nmap Scripting Engine / RustScan Activity Detected

## Description

This detection identifies potential **network reconnaissance and scanning activity** by monitoring suspicious usage of **Nmap Scripting Engine (NSE)** and **RustScan** through endpoint network telemetry.

Attackers commonly leverage tools such as **Nmap** with scripting (`--script`) or **RustScan** to perform:
- Advanced service enumeration
- Vulnerability discovery

The rule inspects `DeviceNetworkEvents` for indicators that scanning activity originated **from an endpoint**, which may indicate:
- Compromised internal hosts performing reconnaissance
- Unauthorized penetration testing tools
- Red team or adversary post-compromise activity

## Log Source

- **Table:** DeviceNetworkEvents  
- **Data Required:**  
  - Endpoint network telemetry  
  - Initiating process command-line logging
 
## Configuration

- Recommended query scheduling frequency: 15 minutes
- Recommended lookup period: 15 minutes

## Entity Mapping
- Hostname: DeviceName
- Source IP: LocalIP
- Destination IP: RemoteIP
- Process Command Line: InitiatingProcessCommandLine
