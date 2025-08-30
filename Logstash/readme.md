# Logstash Collector for Microsoft Sentinel

This guide explains how to configure **Logstash** as a collector for Microsoft Sentinel.  
The goal is to provide flexibility when ingesting logs into Sentinel, especially in cases where Microsoft’s native collectors are limited or when you need a centralized approach without having a lot of agents in your environment.

<img width="712" height="475" alt="image" src="https://github.com/user-attachments/assets/f8a298dc-8392-46b8-a7a6-678541e4068f" />

---

## Recommended Use Cases

### 1. Centralized Collector for Multiple SIEMs
- If you manage multiple SIEMs and don’t want to install agents (e.g., **AMA Agent**) directly on endpoints.  
- Instead:
  - Use **Winlogbeat** to forward Windows logs into **Logstash**.
  - Forward Syslog data (from Linux or network devices) into **Logstash**.
  - Logstash forwards everything into **Microsoft Sentinel**.
- Deploy **two Logstash servers** for redundancy.

### 2. Unsupported or Poorly Parsed Logs
- Sometimes Microsoft’s collectors:
  - Do **not collect rare syslog formats**, or
  - **Fail to parse logs correctly**.
- A **Logstash collector** allows you to normalize, enrich, and transform these logs before ingesting them into Sentinel.

### 3. Multi-SIEM log distribution
- If your organization uses multiple SIEMs, you can use Logstash as a universal collector and distributor.
- Configure multiple Logstash pipelines to send the same logs to different SIEMs. 
- Alternatively, use Kafka + Logstash for scalable log distribution, ensuring logs from all sources can be routed “from everything to everywher
---

## Logstash Architecture

The Logstash engine is composed of three components:

1. **Input plugins** – Customized collection of data from various sources.  
2. **Filter plugins** – Manipulation and normalization of data according to specified criteria.  
3. **Output plugins** – Customized sending of collected and processed data to various destinations.  

---

## Prerequisites

- **Logstash installed** on a dedicated server.
  - Supported versions for the Sentinel output plugin:
    - `7.0 – 7.17.13`
    - `8.0 – 8.9`
    - `8.11 – 8.15`
  - If using **Logstash 8**, disable **ECS** in your pipeline.

- **Microsoft Sentinel Workspace**
  - Ensure you have **Contributor rights**.

- **Permissions**
  - You must have rights to **create Data Collection Rules (DCRs)**.

- **Microsoft Sentinel Logstash Output Plugin**
  - Install the official plugin:  
    `https://github.com/Azure/Azure-Sentinel/tree/master/DataConnectors/microsoft-sentinel-log-analytics-logstash-output-plugin`
  - If you cannot install directly, a manual `.zip` installation can be used.

---

##  Step 1 – Configure Logstash Inputs

Define your **inputs** (Winlogbeat, Syslog, etc.). Example:

conf
input {
  # Winlogbeat (Windows logs)
  beats {
    port => 5044
  }

  # Syslog (Linux/network devices)
  tcp {
    port => 514
    type => syslog
  }
}

## Step 2 – Generate Sample Files

Before ingestion, create sample log files from each data source. These are needed when creating DCR transformations.

Example output configuration:

`output {
  microsoft-sentinel-log-analytics-logstash-output-plugin {
    create_sample_file => true
    sample_file_path   => "/tmp"   # or "C:\\temp" on Windows
  }
}`

Run Logstash temporarily with this config until the sample files are created.

Collect at least a few lines of real logs in the sample file:
- One sample for Winlogbeat (Windows).
- One sample for Syslog (Linux/devices/network devices).

## Step 3 – Create an Application Registration

In Microsoft Entra ID (Azure AD):
1. Go to App registrations → New registration.
2. Record the:
- Tenant ID
- Client ID
- Client Secret
## Step 4 – Create Data Collection Rules (DCRs)

In the Azure Portal -> Data Collection Rules.

1. Create a new DCR and target your Log Analytics workspace.
2. In the Transformations tab:
3. Upload your sample file. 
- Apply the WindowsEvent transformation or
- Repeat with your Syslog sample file and apply the Syslog transformation 
- Ensure TimeGenerated is correctly mapped in each transformation.

- Syslog example transformation

When creating the transformation for Syslog, open the DCR template JSON (Export -> Edit template) and set the transformation block like this:

`{
  "transformKql": "source | project TimeGenerated = ls_timestamp, EventTime = todatetime(timestamp), Computer = logsource, HostName = logsource, HostIP = host, SyslogMessage = message, Facility = facility_label, SeverityLevel = severity_label",
  "outputStream": "Microsoft-Syslog"
}`
This standardizes output into the Syslog table (Microsoft-Syslog).

Important: TimeGenerated must be present and a valid datetime; otherwise ingestion and analytics will be misaligned.

## Step 5 – Assign IAM Roles on the DCR

1. Open the DCR resource in Azure.
2. Go to Access control (IAM).
3. Assign the role "Monitoring Metrics Contributor" to the application registration created in Step 3.

## Step 6 – Configure Logstash Output

Configure Logstash to send to your Data Collection Endpoint (DCE) using the DCR you created:

`output {
  microsoft-sentinel-log-analytics-logstash-output-plugin {
    client_app_Id            => "<your client_app_id>"
    client_app_secret        => "<your client_app_secret>"
    tenant_id                => "<your tenant_id>"
    data_collection_endpoint => "<your logsIngestion URI>"
    dcr_immutable_id         => "<your DCR immutableId>"
    dcr_stream_name          => "<your DCR stream name>"
    create_sample_file       => false
    sample_file_path         => "C:\\temp"
    proxy                    => "http://proxy.example.com"
  }
}`

## Parameter reference
Parameter	Description
client_app_Id	The Application (client) ID from your app registration (Step 3).
client_app_secret	The client secret created for the app registration (Step 3).
tenant_id	Your tenant ID (Microsoft Entra ID → Overview).
data_collection_endpoint	The logsIngestion URI of your Data Collection Endpoint (DCE).
dcr_immutable_id	The DCR immutableId (visible in the DCR Overview → JSON view).
dcr_stream_name	Must match the DCR stream. For standard tables this is typically Microsoft-Syslog or Microsoft-WindowsEvent. If your DCR uses a custom stream name (for example Custom-SyslogStream), copy it exactly from dataFlows > streams in the DCR JSON.

After you finish configuration, restart the Logstash service.

## Step 7 – Firewall and Proxy Requirements

Allow outbound HTTPS to the following endpoints. If Azure virtual network service tags cannot be used, open these explicitly.

<img width="1208" height="521" alt="image" src="https://github.com/user-attachments/assets/1315deca-71c1-4450-8432-87712e06a16b" />

If your environment uses SSL inspection, create explicit bypass rules for these endpoints.

## Verification

1. Restart Logstash and check the Logstash logs for any connection or auth errors.
2. In Log Analytics, query the target tables:
- `WindowsEvent | take 50`
       or
- `Syslog | take 50`
3. Validate that TimeGenerated aligns with event times and that key fields are populated.

## Reference

Microsoft Sentinel – Logstash data connection rules:
https://learn.microsoft.com/en-us/azure/sentinel/connect-logstash-data-connection-rules


