# McAfeeProxyParser

## Description
This parser extracts and normalizes proxy-related events from the **CommonSecurityLog** table within Microsoft Sentinel for **McAfee Web Gateway**.  
It enhances the raw logs by mapping HTTP status codes, block reasons, virus detections, reputation, and policy details into structured fields.  
This allows for improved **threat detection**, **URL category analysis**, and **investigation of web traffic anomalies**.  

## Log Source
- **Table:** CommonSecurityLog  
- **Vendor:** McAfee  
- **Product:** Web Gateway  
