# Suspicious Ngrok or Equinox Tunnel Usage (Process & Network Correlation)

## Description

This detection identifies potentially **unauthorized or malicious usage of tunneling services** such as **Ngrok** or **Equinox** by correlating **process execution** and **network activity** on endpoints.

Tunneling tools like Ngrok are frequently abused by attackers to:
- Expose internal services to the internet
- Bypass firewall and NAT controls
- Establish command-and-control (C2) channels
- Facilitate data exfiltration or lateral movement

The rule searches for indicators of Ngrok-related activity across both **DeviceNetworkEvents** and **DeviceProcessEvents**, then correlates them on the same host to increase detection confidence.

## Log Source

- **Table:** DeviceNetworkEvents  
- **Table:** DeviceProcessEvents  
- **Data Source:** Microsoft Defender for Endpoint  

## Detection Logic

This detection works in three stages:

1. **Network Events**
   - Identifies suspicious outbound connections or metadata containing:
     - `ngrok`
     - `equinox.io`
   - Searches across URLs, additional fields, process names, and action types

2. **Process Events**
   - Identifies suspicious process executions referencing tunneling services
   - Searches command lines, initiating process chains, file paths, and file names

3. **Correlation**
   - Joins network and process activity on the same device
   - Reduces false positives and highlights active tunneling behavior

## Configuration

- Recommended query scheduling frequency: 15 minutes
- Recommended lookup period: 1 hour
- Severity Recommendation: High

# MITRE ATT&CK Mapping

- T1572 – Protocol Tunneling
- T1071.001 – Application Layer Protocol: Web Protocols
- T1105 – Ingress Tool Transfer

## Recommendations / Tuning

Ngrok may be legitimately used by:
- Developers
- Internal testing environments
- Authorized penetration testing teams


