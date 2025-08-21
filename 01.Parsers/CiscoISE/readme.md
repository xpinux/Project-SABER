# **Parser: CiscoISE**

## **Description**
This parser is an **enhanced version of the Microsoft-supplied Cisco ISE Syslog parser**, which is currently **not updated** in the Microsoft Sentinel content store.  

It extracts and normalizes key security events from **Syslog** within Microsoft Sentinel, providing structured fields for better **threat detection and investigation**.  

Key enhancements include:  
- **EventID extraction** from Cisco ISE events (crucial for alerts such as **certificate expiration monitoring**)  
- **Normalization of security events** for consistent field mappings  
- **Improved support for detection engineering, hunting queries, and analytical rules**  

---

## **Log Source**
- **Table:** `CommonSecurityLog`
- **Vendor:** `Cisco`
- **Product:** `Cisco ISE`

---

## **Benefits**
- More accurate and reliable alerting  
- Enhanced visibility into Cisco ISE events  
- Facilitates proactive monitoring, hunting, and response  

---
