# Logstash Collector for Microsoft Sentinel

This guide explains how to configure **Logstash** as a collector for Microsoft Sentinel.  
The goal is to provide flexibility when ingesting logs into Sentinel, especially in cases where Microsoft’s native collectors are limited or when you need a centralized approach without having a lot of agents in your enviroment.

---

## 📌 Recommended Use Cases

### 1. Centralized Collector for Multiple SIEMs
- If you manage multiple SIEMs and don’t want to install agents (e.g., **Winlogbeat**) directly on endpoints.  
- Instead:
  - Use **Winlogbeat** to forward Windows logs into **Logstash**.
  - Forward syslog data (from Linux or network devices) into **Logstash**.
  - Logstash forwards everything into **Microsoft Sentinel**.
- Deploy **two Logstash servers** for redundancy.

### 2. Unsupported or Poorly Parsed Logs
- Sometimes Microsoft’s collectors:
  - Do **not collect rare syslog formats**, or
  - **Fail to parse logs correctly**.
- A **Logstash collector** allows you to normalize, enrich, and transform these logs before ingesting them into Sentinel.

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
    [Docs link](https://learn.microsoft.com/azure/sentinel/connect-logstash-data-connection-rules)  
  - If you cannot install directly, a manual `.zip` installation can be used.

---

## Step 1 – Configure Logstash Inputs

Define your **inputs** (Winlogbeat, Syslog, etc.). Example:

```conf
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
} ```

## Step 2 – Generate Sample Files

Before ingestion, create sample log files from each data source.
These are needed when creating DCR transformations.

Example output configuration:

```output {
  microsoft-sentinel-log-analytics-logstash-output-plugin {
    create_sample_file => true
    sample_file_path   => "/tmp"   # or "C:\\temp" on Windows
  }
}```

- Run Logstash temporarily with this config.
- Collect at least a few lines of real logs in the sample file:
- One sample for Winlogbeat (Windows).
- One sample for Syslog (Linux/devices/network devices).

## Step 3 – Create an Application Registration

In Microsoft Entra ID (Azure AD):

1. Go to App Registrations → New Registration.

2. Record the:

- Tenant ID

- Client ID

- Client Secret

3. Assign API permissions for Log Analytics ingestion.

## Step 4 – Create Data Collection Rules (DCRs)

1. In the Azure Portal -> Data Collection Rules.

2. Create a new DCR.

3. In the Transformations tab:

4. Upload your Winlogbeat sample file.

5. Apply the WindowsEvent transformation 

- Repeat with your Syslog sample file and Syslog transformation.

` Important:
Make sure TimeGenerated is properly mapped, otherwise logs won’t align correctly in Sentinel. `

## Step 6 – Assign IAM Roles

1. Open the DCR Resource in Azure.

2. Go to IAM.

Assign the role:

- Monitoring Metrics Contributor

To the Application Registration you created earlier.

Step 7 – Configure Logstash Output

After the app registration is ready, configure Logstash to forward logs to Sentinel:
` output {
    microsoft-sentinel-log-analytics-logstash-output-plugin {
      client_app_Id => "<enter your client_app_id value here>"
      client_app_secret => "<enter your client_app_secret value here>"
      tenant_id => "<enter your tenant id here> "
      data_collection_endpoint => "<enter your logsIngestion URI here> "
      dcr_immutable_id => "<enter your DCR immutableId here> "
      dcr_stream_name => "<enter your stream name here> "
      create_sample_file=> false
      sample_file_path => "c:\\temp"
      proxy => "http://proxy.example.com"
    }
}
`
## Final Notes

Always configure at least two Logstash collectors for redundancy.

Using Logstash gives you:

- Full flexibility in log transformations.

- Ability to ingest non-standard logs.

- A central place to manage log ingestion across environments.
