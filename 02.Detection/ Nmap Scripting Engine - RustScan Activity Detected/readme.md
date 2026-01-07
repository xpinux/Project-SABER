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
 
## Configuration

- Recommended query scheduling frequency: 15 minutes
- Recommended lookup period: 15 minutes

## Entity Mapping
- Hostname: DeviceName
- Source IP: LocalIP
- Destination IP: RemoteIP
- Process Command Line: InitiatingProcessCommandLine

## MITRE ATT&CK Mapping

This detection aligns with the following MITRE ATT&CK techniques:

- T1046 – Network Service Discovery
- T1018 – Remote System Discovery
  
## Recommendations / Tuning

This detection is intentionally broad and may generate noise in environments with legitimate scanning activity.

Exclude known and approved scanning sources, such as:
- Penetration testing endpoints
- Vulnerability scanning servers
- Red team tooling hosts
- Security automation systems
