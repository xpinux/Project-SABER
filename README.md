# **Project-SABER**   
```
  _________   _____ _______________________________  
 /   _____/  /  _  \\______   \_   _____/\______   \  
 \_____  \  /  /_\  \|    |  _/|    __)_  |       _/  
 /        \/    |    \    |   \|        \ |    |   \  
/_______  /\____|__  /______  /_______  / |____|_  /  
        \/         \/       \/        \/         \/   
```
### **Sentinel Adversary Behavior & Event Recognition**  

Project-SABER is an open-source repository of **Microsoft Sentinel or Defender Unified Portal KQL queries** designed for **enhanced detection, threat hunting, and event analysis**.  

##  **What’s Inside?**  
- **Analytical Rules** – Proactive threat detection with KQL  
- **Hunting Queries** – Advanced threat investigation techniques
- **Parsers** – Data normalization to enhance log visibility
- **More to come**

## **Why Use SABER?**  
- **Strengthen your security posture** in Microsoft Sentinel  
- **Improve detection engineering** with curated KQL queries
- **Use Parsers for log analysis or detection engineering** 

## **Getting Started**  
1. Explore the directories
2. Implement the KQL queries in **Microsoft Sentinel** or  **Defender XDR**

## **Key Contributors**  
First and foremost, a huge shout-out to **Michalis Michalos (cyb3rmik3)** my ultimate KQL inspiration and the reason this project exists. 

This project also draws inspiration from several amazing members of the Sentinel community. Some queries here may resemble theirs but in true **Project-SABER fashion**, they’ve been **enhanced, modified, or jazzed up** a bit.  

If I’ve “borrowed” a query and forgotten its origin (my notebooks are overflowing, okay 😅), I sincerely apologize in advance!  

Here are some of the **key contributors whose KQL content is publicly available on GitHub**:

- **Bert-Jan Piet (Bert-JanP)** 
- **Rod Trent** – KQL search & Sentinel advocate  
- **Cyb3r-Monk (Mehmet Ergene)** – Creator of one of the most complete KQL courses  
- **Cyb3rWard0g** – Advanced hunting & APT detection  
- **FalconForceTeam / FalconFriday** – MITRE-mapped threat hunting content  
- **SlimKQL / Hunting-Queries-Detection-Rules** – Curated Sentinel KQL queries  

This section is meant to **celebrate the community**, not compete with it—without these incredible contributors, Project-SABER wouldn’t exist.  

##  **KQL Basics**  
Kusto Query Language (KQL) is used in Microsoft Sentinel for querying logs and creating detection rules. Below is an introduction to KQL syntax, operators, and examples.

### **Basic Syntax & Structure**  
A simple KQL query consists of a **table reference**, followed by **filters**, **transformations**, and **aggregations**.

```kql
SecurityEvent
| where EventID == 4625
| project TimeGenerated, Account, Computer
```

### **Common Operators**  
- `where` – Filters data based on conditions.
- `extend` – Adds new calculated fields.
- `ago` – Returns the time offset relative to the time the query executes
- `project` – Selects specific columns.
- `summarize` – Aggregates data (e.g., counts, sums).
- `join` – Combines data from multiple tables.
- `parse` – Extracts data from unstructured text.
- `contains/has` – Looks for any substring match - Looks for a specific word

### **Example Queries**  
Find failed logon attempts:
```kql
SecurityEvent
| where EventID == 4625
| summarize count() by Account, bin(TimeGenerated, 1h)
```

Find unusual process creation events:
```kql
DeviceProcessEvents
| where ProcessCommandLine contains "powershell"
| summarize count() by InitiatingProcessAccountName
```

---

##  **Detection Engineering**  
Detection Engineering involves creating **efficient and accurate** detection rules to identify malicious activity in security logs. 

### **Key Concepts**  
- **Behavioral Detection** – Identify patterns of malicious activity.
- **Tuning Detections** – Reduce false positives by refining queries.
- **Threat Intelligence Integration** – Enrich detections with external threat data.
- **Correlation** – Combine multiple data sources to detect complex attack chains.

### **Best Practices for Detection Engineering**  
1. Use **efficient filtering** (`where` instead of `search` where possible).
2. Minimize **performance impact** (avoid unnecessary `join`s).
3. Optimize queries with **summarization** (`summarize` to reduce dataset size).
4. Include **contextual data** to improve analyst understanding.
5. Continuously **test and refine** detections to minimize noise.

---

##  **Understanding Parsers in KQL**  
Parsers are used in KQL to extract structured data from unstructured logs. This helps in normalizing logs and making them more useful for threat detection.

### **Common Parsing Methods**  
- `extract()` – Uses regex to extract data.
- `parse-kv()` – Parses key-value formatted data.
- `parse` – Extracts fields from structured strings.
- It is very important to escape special characters when dealing with Regex. In KQL we can do it with these 2 options:
  
1. Escape the \ character with double \: \\
2. Use verbatim string: @

### **Example: Extracting Data with `extract()`**  
```kql
let log = "User=admin IP=192.168.1.1 Action=FailedLogin";
print extract(@"IP=(\d+\.\d+.\d+\.\d+))", 1, log)
```
Output:
```
192.168.1.1
```

Using `parse-kv()` to extract fields:
```kql
let log = "User=admin;IP=192.168.1.1;Action=FailedLogin";
print parse-kv(log, ";", "=")
```

Parsers are **essential** for normalizing logs and making them usable in detection rules.

---

## **Contributions**  
Have a **KQL query** that can improve detections? Submit a **pull request** and contribute to the community!  
