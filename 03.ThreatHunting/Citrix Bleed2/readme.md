# Citrix Bleed2 Exploitation Attempts – `/p/u/doAuthentication.do`

## Description
This hunting query identifies potential exploitation attempts of **Citrix Bleed2 (CVE-2023-4966 / CVE-2023-6548)** by detecting traffic targeting the endpoint `/p/u/doAuthentication.do`.  

Attackers may exploit this endpoint to:
- Leak session tokens  
- Bypass authentication  
- Conduct credential theft or session hijacking  

Key points:
- Correlates across **Syslog** and **CommonSecurityLog**  
- Focuses on requests that were **not blocked/mitigated**  
- Will generate significant noise in Citrix environments, requiring tuning  

## Log Source
- **Tables:**  
  - `Syslog` (from Citrix appliances / load balancers)  
  - `CommonSecurityLog` (from firewalls, WAFs, or proxies)
    
## MITRE ATT&CK Mapping
- **T1190 – Exploit Public-Facing Application**  
- **T1078 – Valid Accounts (if session tokens are hijacked)**  
- **T1556 – Modify Authentication Process**  

