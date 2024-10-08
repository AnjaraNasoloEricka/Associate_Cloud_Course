# 4- Logging and Monitoring +  Networking + Security

## Cloud logging 
- **Log** : information generated by applicative layer

### Routing of logs 
- Logs can be routed to a variety of sink : 
    - Cloud Storage 
    - BigQuery 
    - Pub/Sub topic 

Two sinks for each Cloud project, billing account, folder and organization : 
- **_required** (400 days, change not allowed) - essential and critical 
- **_default** (30-day default, Custom retention between 1 day and 3650 days) - other information - need activation and paid

### Structured logging
- Log are structure in `json` format

- Structure logging refers to log entries that use the jsonPayload field to add structure to ther payloads rather than textPayload so content is indexed

### Log based-metrics 
- Log based-metrics are derive metric data from the content of log entries 
- **Examples :**
    - Count the number of log entries that contain a particular message 
    - Extract latency information recorded in log entries 
- **Data types :**
    - **Counter :** # of log entries in a period
    - **Distribution :** collect into histogram buckets
    - **Boolean :** `True` if query matches a log entry, false otherwise

### Cloud Audit Log 
- Help you answer the questions : `Who did what , where, when ?` with your Google Cloud resources 

- **Types :**
    - `Admin activity aufit log` : actions that modify the configuration or metadata of resources
    - `Data access audit log` : calls that read the configuration metadata resources
    - `System event audit log` : generated by Google systems 
    - `Policy Denied audit log` : recorded when a Google Cloud Service denies access to a user or service account because of security policy intention

### Asset Inventory 

- **Terraform** : Infrastructure as Code

- **Asset Inventory** : provides inventory services based on a time series database 

- **Features of Asset Inventory :**
    - Search assets and monitory asset changes 
    - Export asset history to BigQuery and Cloud Storage 
        - Data is kept for 30 days or the last asset status
    - Create custom inventory reports
    
### Error logging : error reporting to minimize error

### Query langage 
Your query log through the CLI and via the console 
- you use query in the console to get the information you need
- based in **NQL** (Nexthink Query Language) Language
    - Example : 
        ```nql
        resource_type="audited_resource"
        severity="notice"
        ```
### Log Analytics 
- In case you don't know the NQL Language, Google created the `Log Analytics` which works with `SQL`
- Log Analytics let you use BigQuery to query your data 
- To perform aggregate operations, enable analytics on the log bucket and then use analytics on the logs bucket and then use Log Analytics SQL 

## Monitoring
Cloud Monitoring collects metrics, events and metadata from Google Cloud, hosted uptime probes and application instrumentation.

### Features 
- Log based-metrics 
- Charts and dashboard 
- Alerting policies 
- View and monitor the time-series data 

### Multi-project scopes
- Lets you view and manage metrics in the following ways : 
    - For a single project 
    - For multiple projects within a single organization 
    - For multiple projects across multiple organizations
    - For multiple Google Cloud projects and AWS accounts 

### Resource Group 
- Cloud Monitoring lets you define a set of resources (for example a set of microservices) into a group 

### Managed Prometheus
- **Prometheus** : monitoring solution 
- Google offers a fully managed multi-cloud solution for Prometheus Metrics 
- You can use `PromQL` to monitor your data 

### SLO Monitoring Framework 
#### Difference between SLO and SLA 
- **SLO** : Service Level Objective
- **SLA** : Service Level Agreement

#### Product 
- Google offers product to see the SLO (HA and no latency)

### Uptime Checks 
- Here you define test, to check if your app is in the state you need (it returns HTTP status to tell the state of your app)
- **Types :**
    - `Public uptime checks` : issue requests from multiple locations throughout the world to publicly available URLs or GCloud resources 
    - `Private uptime checks` : issue requests to internal IP addresses of Google Cloud resources 

#### Synthetic Monitoring 
- Capacity of uptime checks to send http requests 

### Tracing 
- Used for user experience 
    - how long do requests take ? 
    - where are we experiencing latency ?
    - what can be improved ? 

### Active Assist 
- Portfolio of tools thaht use data intelligence, and machine learning ro reduce cloud complexity and administrative work 

## Alerting 
### Aspects 
- Alerting policies : based on time-series or log data 
- Incidents 
- Notification channel

### How to define alert ?
You can define alert by queries, via : 
- PromQL 
- SQL 

### Types of alert 
- Budget (for pricing)
- Log-based alerts 

## Google Cloud Security 
- Check Security.md on Cloud Infrastructure folder

> Note : `supply chain` means attack the provider instead of the main competitor