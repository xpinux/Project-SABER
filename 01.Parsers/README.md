# Parsers

This folder contains **KQL parsers** for Microsoft Sentinel to enhance log normalization and structured data extraction. Our parsers improve upon existing log formats, including **CommonSecurityLog** and **Syslog**, ensuring cleaner and more efficient threat detection.

## **What’s Inside?**
- **Enhanced CommonSecurityLog Parsers** – Refining already-parsed logs for better accuracy.
- **Full Syslog Parsers** – Completely parsing raw Syslog data into structured fields.
- **Other Custom Parsers** – Additional log sources optimized for Microsoft Sentinel.

## **How to Save and Use a KQL Parser**
To use a parser effectively in Microsoft Sentinel:

### **Save the Parser as a Function**
1. Open **Microsoft Sentinel**.
2. Navigate to **Logs**.
3. Paste the KQL parser query into the query window.
4. Click **Save As** → **Save as function**.
5. Assign a **relevant name** to the parser (e.g., `NaomiParser`).

