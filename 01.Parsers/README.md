# Parsers

This folder contains **KQL parsers** for Microsoft Sentinel to enhance log normalization and structured data extraction. Our parsers improve upon existing log formats, including **CommonSecurityLog** and **Syslog**, ensuring cleaner and more efficient threat detection.

# Note on Parsers
These Parsers improve uppon existing log formats, but are not limited by them. The code logic, hides behind the KQL and it largely contains the logic of regex in order to parse logs. If you ingest a System/Log in other way (**Like Logstash**) it would be usefull to check the code for the systems that you are intersted and to Copy the code of the fields of your choosing (Changing the Source Table Name and making a few adjustments). Most of the Syslog Parsers can be used also for **Logstash** if you ingest correctly the **SyslogMessage** field.

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

