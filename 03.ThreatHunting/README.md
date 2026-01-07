# Threat Hunting

## Overview

This folder contains **threat hunting queries and investigations** focused on proactive detection of attacker activity that may not yet be covered by traditional detection rules.  

Each subfolder contains a focused hunting use case with:
- a **clear intent** (e.g., supply chain compromise, brute force, command abuse)
- one or more **hunting queries**
- tuning guidance, exclusions, and recommendations.

Hunting queries in this repo are designed to help analysts:
- discover **anomalous behavior** missed by automated analytics
- investigate **patterns of suspicious activity**
- refine and evolve detections based on real data

## How to Use

1. **Understand the use case:**  
   Before running a query, read the subfolder’s README to understand what the hunt is looking for and why. Each query has a specific goal (e.g., supply chain abuse, credential theft, reconnaissance).  

2. **Run interactively:**  
   Use your SIEM (Log Analytics / Sentinel Logs) to run queries interactively. Inspect the results and enrich them with context (user, host, network).  

3. **Tune with exclusions:**  
   Hunting queries are often broad by design and may capture benign activity in high-volume environments.  
   - Add host or account exclusions  
   - Limit to specific timeframes or attacker IOAs  
   - Adjust thresholds or command conditions

4. **Pivot and investigate:**  
   Use results as starting points for deeper investigation. Build follow-ups that explore parent processes, related network activity, or escalation patterns.

5. **Operationalize:**  
   Once a pattern proves malicious and repetitive, consider translating the hunt into a **scheduled detection rule** (in `/detections/`) with tuned thresholds and alerting.
