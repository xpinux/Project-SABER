## License Expiration

## Description

This detection identifies log messages related to **license expiration**, **subscription termination**, **activation failures**, and **licensing compliance issues** across infrastructure and security devices.

Licensing issues can lead to:
- Disabled or degraded security controls
- Loss of visibility or enforcement
- Service outages or reduced functionality
- Compliance violations

Attackers may also intentionally disrupt licensing mechanisms to weaken defensive capabilities or mask malicious activity.

This rule scans multiple log sources for known license-related error and warning patterns.

## Data Sources

### Tables
- `Syslog`
- `CommonSecurityLog`

## Detection Logic

- Matches against a comprehensive keyword list covering:
  - License expiration
  - Subscription termination
  - Activation and validation failures
  - Compliance and entitlement issues
- Correlates logs across multiple data sources
- Excludes known benign update-related failures
- Surfaces vendor and host context for triage

## Recommended Rule Configuration

- **Query frequency:** 30 minutes  
- **Lookup period:** 24 hours  
- **Recommended severity:** Medium - Low

## MITRE ATT&CK Mapping

### Primary Techniques
- **T1562 – Impair Defenses**
  - Disabling or degrading security tooling due to license failure

## Known False Positives

- Wireless LAN Controller (WLC) compliance messages
- Non-security product license warnings
- Informational license renewal notifications
- Temporary activation server connectivity issues

## Recommendations / Tuning

### Exclusions

Consider excluding:
- Known non-security devices (e.g., printers, lab equipment)
- Vendors that generate noisy compliance warnings
- Specific message patterns (e.g., `"WLC compliance errors"`)

