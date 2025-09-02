# Mimikatz-Detection

## Description
This detection identifies potential **Mimikatz** execution or related credential dumping techniques.  
It inspects the `SecurityEvent` table for suspicious command-line strings associated with Mimikatz and other credential theft tools.  

Mimikatz is a widely used tool by attackers for extracting plaintext credentials, Kerberos tickets, and other authentication material. Detecting its presence is crucial as it usually indicates an **active compromise**.

## Log Source
- **Table:** SecurityEvent  
- **Field:** CommandLine  

## Detection Logic
The query searches for known suspicious command-line patterns, including:
- `lsadump::sam`
- `mimidrv sys`
- `Mimikatz`
- `privilege::debug`
- `sekurlsa::logonpasswords`
- `"<3 eg.oe"`
- `"eo.oe.oe"`

## Configuration
- **Recommended query scheduling frequency:** 1 hour  
- **Recommended lookup period:** 1 hour  
- **Severity Recommendation:** High  

## Entity Mapping
- AccountName  
- DeviceName
- CommandLine

## MITRE ATT&CK Mapping
- **T1003 – OS Credential Dumping**  
- **T1003.001 – LSASS Memory** 

## Recommendations
- Use **simulate results** in Sentinel to test this rule before enabling it in production.  
- Fine-tune by excluding **administrative test accounts** or **lab environments** if necessary.  
- Investigate immediately if triggered — these strings almost always indicate **malicious activity**.
