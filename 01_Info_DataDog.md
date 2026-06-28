# What is Datadog?

* Datadog is a monitoring service for cloud-scale applications, providing monitoring of servers, databases, tools, and services, through a SaaS-based data analytics platform.

* They built Datadog to be a cloud infrastructure monitoring service, with a dashboard, alerting, and visualizations of metrics.

* Datadog was listed in Forbes’ Cloud 100 and was ranked in the top ten fastest growing companies in North America in Deloitte's 2016 Fast 500 List.

* Datadog was founded in 2010 by Olivier Pomel and Alexis Lê-Quôc.

---

# Why Datadog?
> Datadog is used to **monitor, troubleshoot, and improve the health and performance** of applications, servers, databases, cloud infrastructure, containers, and services—all from a single platform.

Without monitoring, you don't know:

* Is the application running?
* Is the server healthy?
* Is the database slow?
* Is the CPU overloaded?
* Did the deployment fail?
* Why are users getting errors?

Datadog answers all of these questions.

---
# Real-Time Example:
Imagine your company has an online shopping application.

```
Customer
    |
    v
Website
    |
    v
Application Server
    |
    v
Oracle Database
```

One day, customers complain:

> "The website is very slow."

How do you know where the problem is?

**Without Datadog:**
* Login to Server 1
* Check CPU
* Login to Server 2
* Check Memory
* Login to Database
* Check queries
* Check logs
* Takes 30–60 minutes

**With Datadog:**
* Open one dashboard
* Immediately see:

  * CPU = 98%
  * Memory = 95%
  * Database response time = High
  * Error rate increased
  * Alert already sent

Problem found in **2–3 minutes**.

---
# Why Companies Use Datadog:
### 1. Infrastructure Monitoring

**Monitor:**
* Linux Servers
* Windows Servers
* Virtual Machines
* Cloud Instances

Example:
```
Server CPU = 95%

Datadog Alert

"CPU usage exceeded 90%"
```

---
### 2. Application Monitoring (APM):
Checks:
* API response time
* Request latency
* Error percentage
* Slow transactions

Example:
```
Login API

Normal Time
200 ms

Today
2500 ms

Datadog shows exactly where the delay occurs.
```

---
### 3. Database Monitoring:
Supports databases like:

* Oracle
* MySQL
* PostgreSQL
* SQL Server
* Cloud Spanner
* MongoDB

Example:
```
Oracle Database

CPU = 98%
Connections = 500
Slow Queries = 25

Datadog Dashboard shows everything.
```

---
### 4. Log Monitoring:
Instead of logging into servers:

```
SSH
cat application.log
grep ERROR
```

Datadog collects logs automatically.

Search:

```
ERROR
```

Result:

```
Application Failed

Time
Server
Reason
```

---
### 5. Alerting:
Suppose CPU becomes high.

Datadog automatically sends:

* Email
* Slack
* Microsoft Teams
* PagerDuty
* SMS (with integrations)

Example

```
CPU > 90%

↓

Alert Generated

↓

DevOps Engineer receives notification
```

---
### 6. Dashboard:
All monitoring data is available in one place.

Example Dashboard:
```
CPU Usage
Memory
Disk
Network
Database
Application Errors
API Latency
Containers
Kubernetes
```

No need to log into multiple systems.

---
### 7. Cloud Monitoring:
Supports:

* AWS
* Azure
* GCP

Example:
```
Google Cloud VM

↓

Datadog Agent

↓

Metrics

↓

Dashboard
```

---
### 8. Container Monitoring:
**Supports:**

* Docker
* Kubernetes
* GKE
* EKS
* AKS

Shows:

* Running Pods
* Failed Pods
* CPU
* Memory
* Restarts

---
### 9. CI/CD Monitoring:
Integrates with:

* Jenkins
* GitHub Actions
* Harness
* GitLab CI

Example

```
Deployment Failed

↓

Datadog Alert

↓

Pipeline details visible
```

---
### 10. Security Monitoring:
Detects:

* Unauthorized access
* Suspicious login attempts
* Configuration changes
* Security events

---

# Why is Datadog Important for DevOps?

As a DevOps Engineer, your responsibilities include:

* Monitoring servers
* Monitoring applications
* Monitoring databases
* Monitoring Kubernetes clusters
* Monitoring cloud infrastructure
* Setting alerts
* Creating dashboards
* Troubleshooting production issues

Datadog helps you perform all of these tasks from a single platform.

---
# Real-Time DevOps Workflow

```
Developer
     |
     v
Code Commit
     |
     v
Harness CI/CD Pipeline
     |
     v
Deploy Application
     |
     v
GCP VM / Kubernetes
     |
     v
Application Running
     |
     v
Datadog Agent
     |
     v
Datadog Platform
     |
     +----------------------+
     |                      |
     v                      v
 Dashboard              Alerts
     |
     v
DevOps Engineer
```

---
# In Your Project (Data Migration)

Based on what you've shared about your project:

* **Source Database:** Oracle
* **Target Database:** Cloud Spanner
* **CDC Tool:** Striim
* **Cloud Platform:** GCP
* **CI/CD:** Harness
* **Monitoring:** Datadog

##### Datadog can monitor:

* Oracle database health
* Cloud Spanner performance
* Striim pipeline status
* GCP VM metrics
* Kubernetes (if used)
* Harness deployment status
* CPU, memory, disk, and network usage
* Application logs and alerts

If any component slows down or fails, Datadog can notify the DevOps team immediately.

---
### Why do we use Datadog?

> Datadog is a cloud-native monitoring and observability platform that provides real-time visibility into infrastructure, applications, databases, logs, and cloud services. It enables DevOps teams to monitor system health, create dashboards, configure alerts, troubleshoot issues quickly, and improve application performance. Datadog integrates with cloud providers, Kubernetes, CI/CD tools, and databases, making it a centralized monitoring solution for modern applications.

---

**Functionality  → Need   → Ease of use   → Hard to replicate**

**1. The Agent** - We don't get nearly enough insight from cloudwatch alone, we need an on-instance tool to gather system and app metrics.

**2. Integrations** - There are lots of services with operational significance, but many of them don't provide a good way to access their data.

**3. Events** - We would spend dramatically longer investigating problems if we had to look at each source of events in isolation. Many of our event sources don't even provide a way for us to view past events or to query them.

**4. Dashboards** - Per-service and per-instance dashboards are important for investigating problems quickly. The consolidation of data from multiple sources is again a key feature.

**5. Alerting** - We need to do analyze trends in our metrics and alert on them.


> Here I described a system of collectd, custom code to pull metrics from cloudwatch, custom code to pull or receive events from various sources (airbrake, cloudtrail, chef, pagerduty, jenkins, etc) influxdb, and grafana.

---

|                 | **Is it Up?**    | **Is it Slow?** | **Is it Broken?** |
| --------------- | ---------------- | --------------- | ----------------- |
|                 | **Availability** | **Performance** | **Reliability**   |
| **Application** | Datadog          | Datadog         | Datadog           |
| **Network**     | Datadog          | Datadog         | Datadog           |
| **Server**      | Datadog          | Datadog         | Datadog           |

---
# Datadog Backend and Datadog Agent

## What is Datadog Agent?

**Datadog Agent** is a lightweight software installed on your server, VM, Kubernetes node, or container that **collects metrics, logs, traces, events, and system information** and sends them securely to the **Datadog Backend**.

### Simple Definition

> **Datadog Agent is a data collector.** It gathers monitoring data from your infrastructure and applications and sends it to the Datadog cloud platform.

---
## What is Datadog Backend?

The **Datadog Backend** is the **cloud platform (SaaS)** where all the data collected by the Datadog Agent is stored, processed, analyzed, and displayed.

The backend provides:

* Dashboards
* Monitoring
* Alerting
* Log Management
* APM (Application Performance Monitoring)
* Infrastructure Monitoring
* Security Monitoring
* Reports

### Simple Definition

> **Datadog Backend is the brain of Datadog.** It receives data from agents, processes it, stores it, and displays it in dashboards.

---
# Architecture:

```text
                Datadog Architecture

+--------------------------------------------------+
|                 Datadog Backend                  |
|--------------------------------------------------|
| Dashboards                                       |
| Alerting                                         |
| Metrics Storage                                  |
| Log Management                                   |
| APM                                              |
| Security Monitoring                              |
| Analytics                                        |
+--------------------------------------------------+
                    ▲
                    │ HTTPS (TLS)
                    │
            Sends Metrics, Logs, Traces
                    │
+---------------------------------------------+
|            Datadog Agent                    |
|---------------------------------------------|
| Collects CPU                                |
| Collects Memory                             |
| Collects Disk                               |
| Collects Network                            |
| Collects Logs                               |
| Collects Application Metrics                |
| Collects Database Metrics                   |
+---------------------------------------------+
                    ▲
                    │
      -------------------------------------
      |             |            |         |
      ▼             ▼            ▼         ▼
 Linux Server   Windows VM   Kubernetes  Oracle DB
```

---
# Datadog Agent Responsibilities:

The Agent performs the following tasks:

* Collects CPU usage
* Collects Memory usage
* Collects Disk usage
* Collects Network statistics
* Collects Process information
* Collects Application logs
* Collects Database metrics
* Collects Kubernetes metrics
* Collects Docker metrics
* Collects Custom application metrics

---
# Datadog Backend Responsibilities:

The Backend performs the following tasks:

* Receives data from Agents
* Stores monitoring data
* Processes metrics
* Creates dashboards
* Generates alerts
* Displays graphs
* Correlates logs and metrics
* Runs analytics
* Sends notifications (Slack, Email, PagerDuty, Teams)

---
# Data Flow:

```text
Application
      │
      ▼
Linux Server
      │
      ▼
Datadog Agent
      │
      │ Collect Metrics
      │ Collect Logs
      │ Collect Traces
      ▼
Internet (HTTPS)
      │
      ▼
Datadog Backend
      │
      ├── Dashboards
      ├── Alerts
      ├── Reports
      ├── Analytics
      └── Notifications
```

---
# Example

Suppose your application is running on a GCP VM.

```text
GCP VM
│
├── CPU = 90%
├── Memory = 80%
├── Disk = 70%
├── Application Error
└── Oracle Database Running
```

The **Datadog Agent** installed on the VM collects:

* CPU = 90%
* Memory = 80%
* Disk = 70%
* Application Logs
* Oracle Database Metrics

The Agent sends this data to the **Datadog Backend**.

The Backend then:

* Displays CPU graphs
* Shows Memory usage
* Displays database performance
* Generates alerts if CPU > 90%
* Sends notifications to Slack or Email

---
# Communication

```text
Server
   │
Datadog Agent
   │
HTTPS (Encrypted)
   │
Datadog Backend
```

Communication is secure using **HTTPS/TLS**.

---
# Real Project Example (Your Data Migration Project):

You mentioned your project uses:

* Oracle Database
* Cloud Spanner
* Striim
* GCP
* Harness
* Datadog

**The architecture could look like this:**

```text
Oracle Database
        │
        ▼
      Striim
        │
        ▼
Cloud Spanner

        │
        ▼
Datadog Agent
        │
        ▼
Datadog Backend
        │
 ┌──────┼───────────────┐
 │      │               │
 ▼      ▼               ▼
Dashboard Alerts     Reports
```

**The Agent can monitor:**

* Oracle database metrics
* Cloud Spanner metrics (through integration)
* Striim process health
* GCP VM metrics
* CPU, Memory, Disk, Network
* Application logs

The Backend displays all this information in one place and alerts the DevOps team if issues occur.

---
# Difference Between Datadog Agent and Datadog Backend:

| Feature              | Datadog Agent                          | Datadog Backend                       |
| -------------------- | -------------------------------------- | ------------------------------------- |
| Runs On              | Server, VM, Kubernetes Node, Container | Datadog Cloud (SaaS)                  |
| Purpose              | Collects monitoring data               | Stores, analyzes, and visualizes data |
| Installed By         | DevOps Team                            | Managed by Datadog                    |
| Collects Metrics     | Yes                                    | No (receives them)                    |
| Collects Logs        | Yes                                    | No (receives them)                    |
| Stores Data          | No                                     | Yes                                   |
| Generates Dashboards | No                                     | Yes                                   |
| Sends Alerts         | No                                     | Yes                                   |
| Managed By           | Customer                               | Datadog                               |

---
# Q: What is the difference between Datadog Agent and Datadog Backend?**

> The **Datadog Agent** is a lightweight software installed on hosts such as VMs, servers, containers, or Kubernetes nodes. It collects metrics, logs, traces, and system information and securely sends them to the Datadog Backend.

>The **Datadog Backend** is the cloud-based SaaS platform that receives, stores, analyzes, and visualizes this data. It provides dashboards, alerting, log management, APM, and analytics, enabling DevOps teams to monitor and troubleshoot their infrastructure and applications from a centralized platform.

---
Absolutely. Since you're learning **Datadog from a DevOps perspective** for your **Data Migration (Oracle → Striim → Cloud Spanner)** project, here are **professional notes** that are easy to understand and useful for interviews and real-world work.

---

# How Does Datadog Collect Data?

## Definition

Datadog collects data by installing a lightweight software called the **Datadog Agent** on servers, virtual machines (VMs), containers, or Kubernetes nodes. The Agent gathers infrastructure metrics, application metrics, logs, traces, and events, then securely sends this information to the **Datadog Backend** (Cloud Platform) for analysis, visualization, and alerting.

---

# End-to-End Data Collection Flow

```text
                Datadog Backend (Cloud)
        +-----------------------------------+
        | Dashboards                        |
        | Alerts                            |
        | Log Management                    |
        | APM                               |
        | Analytics                         |
        +-----------------------------------+
                     ▲
                     │ HTTPS (TLS)
                     │
              Datadog Agent
                     ▲
      ┌──────────────┼──────────────┐
      │              │              │
      ▼              ▼              ▼
 Operating      Applications     Databases
  System        (Java/.NET)      (Oracle,
                                   MySQL,
                                PostgreSQL)
```

---

# Step-by-Step Process

## Step 1: Install Datadog Agent

The Datadog Agent is installed on the machine you want to monitor.

Examples:

* Linux Server
* Windows Server
* GCP VM
* AWS EC2
* Azure VM
* Kubernetes Node
* Docker Host

Once installed, the Agent runs continuously in the background.

---

## Step 2: Collect Infrastructure Metrics

The Agent automatically collects system-level metrics such as:

* CPU Usage
* Memory Usage
* Disk Usage
* Network Traffic
* File System Usage
* Process Information
* System Load

Example:

```text
Linux Server

CPU Usage      : 45%
Memory Usage   : 68%
Disk Usage     : 72%
Network Traffic: 120 Mbps
```

---

## Step 3: Collect Application Metrics

The Agent monitors applications and collects:

* Response Time
* Request Count
* Error Rate
* Throughput
* Application Health

Example:

```text
Java Application

Response Time : 250 ms
Requests/min  : 1200
Errors        : 2
```

---

## Step 4: Collect Logs

The Agent continuously monitors log files.

Example:

```text
Application

     │

application.log

     │

Datadog Agent

     │

Datadog Backend
```

Logs collected include:

* Application Logs
* System Logs
* Web Server Logs
* Security Logs

---

## Step 5: Collect Database Metrics

Datadog provides integrations for databases.

Example:

```text
Oracle Database

Connections
Slow Queries
CPU Usage
Sessions

       │

Datadog Agent

       │

Datadog Backend
```

Supported databases include:

* Oracle
* MySQL
* PostgreSQL
* SQL Server
* MongoDB
* Redis
* Cloud Spanner

---

## Step 6: Collect Kubernetes & Docker Metrics

The Agent monitors containerized environments.

It collects:

* Node Health
* Pod Status
* Container CPU
* Container Memory
* Restart Count
* Cluster Health

---

## Step 7: Send Data to Datadog Backend

After collecting data, the Agent securely sends it to the Datadog Backend using HTTPS/TLS.

```text
Server

   │

Datadog Agent

   │

HTTPS (TLS)

   │

Datadog Backend
```

---

# Types of Data Collected

| Data Type              | Examples                                     |
| ---------------------- | -------------------------------------------- |
| Infrastructure Metrics | CPU, Memory, Disk, Network                   |
| Application Metrics    | Response Time, Throughput, Errors            |
| Logs                   | Application Logs, System Logs                |
| Traces                 | API Calls, Database Calls                    |
| Database Metrics       | Oracle, MySQL, PostgreSQL                    |
| Container Metrics      | Docker, Kubernetes                           |
| Cloud Metrics          | AWS, Azure, GCP                              |
| Events                 | Deployments, Restarts, Configuration Changes |

---

# Data Collection Methods

### 1. Agent-Based Collection

The Datadog Agent collects data directly from the host.

```text
Linux Server

      │

Datadog Agent

      │

Datadog Backend
```

---

### 2. Integration-Based Collection

Datadog has **600+ built-in integrations** that collect data from services like:

* AWS
* GCP
* Azure
* Oracle
* Kubernetes
* Jenkins
* Kafka
* Redis

---

### 3. Log Collection

The Agent reads log files in real time.

```text
Application

      │

application.log

      │

Datadog Agent

      │

Datadog Backend
```

---

### 4. APM (Application Performance Monitoring)

Applications are instrumented with Datadog libraries to collect traces.

```text
User

   │

Application

   │

Database

   │

Trace

   │

Datadog Agent

   │

Datadog Backend
```

---

# Real Project Example (Your Project)

Your project architecture:

```text
Oracle Database
       │
       ▼
     Striim
       │
       ▼
Cloud Spanner
       │
       ▼
Migration Application
       │
       ▼
GCP VM
       │
       ▼
Datadog Agent
       │
       ▼
Datadog Backend
       │
       ├── Dashboards
       ├── Alerts
       ├── Log Explorer
       └── APM
```

The Agent collects:

* GCP VM CPU, Memory, Disk
* Migration Application Logs
* Striim Process Metrics
* Oracle Database Metrics
* Cloud Spanner Metrics
* Network Traffic

---

# Key Points to Remember

* **Datadog Agent** is installed on servers, VMs, containers, or Kubernetes nodes.
* It collects **metrics, logs, traces, events, and process information**.
* It uses **built-in integrations** to monitor databases, cloud platforms, and applications.
* Data is sent securely to the **Datadog Backend** using **HTTPS/TLS**.
* The **Backend** stores the data, creates dashboards, generates alerts, and provides analytics.

---
## Q: How does Datadog collect data?
**Answer:**

> Datadog collects data primarily through the **Datadog Agent**, a lightweight software installed on servers, virtual machines, containers, or Kubernetes nodes. The Agent gathers infrastructure metrics, application metrics, logs, traces, and events. It also uses built-in integrations to collect data from cloud services, databases, and other applications. The collected data is securely transmitted over HTTPS/TLS to the Datadog Backend, where it is stored, analyzed, and visualized through dashboards, monitors, and alerts.

---
## 💡 DevOps Tip

For a DevOps Engineer, remember this simple flow:

```text
Infrastructure/Application
           │
           ▼
    Datadog Agent
 (Collects Monitoring Data)
           │
      HTTPS (TLS)
           │
           ▼
   Datadog Backend
(Store + Analyze + Alert)
           │
           ▼
 Dashboards | Alerts | Logs | APM
```

**One-line formula to remember:**

> Agent = Collects Data → Backend = Stores, Analyzes, Visualizes, and Alerts

---
# How does Datadog work?

### Step 1: Install and Configure the Datadog Agent

Download, install, and configure the **Datadog Agent** on your server, virtual machine (VM), container, or Kubernetes node.

### Step 2: Collect Data

Once the Agent is installed, it starts collecting data from the system and applications, including:

* Metrics
* Logs
* Events
* Traces

The Agent then securely sends this collected data to the **Datadog Backend (Datadog Cloud)** over HTTPS.

### Step 3: Analyze and Visualize Data

The Datadog Backend processes and stores the collected data. You can then use it to:

* Create Dashboards
* Configure Alerts
* Run Queries
* Monitor Infrastructure
* Analyze Logs
* Monitor Application Performance (APM)

---

## Simple Flow

```text
Install Datadog Agent
         │
         ▼
Agent Collects Data
(Metrics, Logs, Events, Traces)
         │
         ▼
Sends Data to Datadog Backend (Cloud)
         │
         ▼
Dashboards | Alerts | Queries | APM | Logs
```

---
> Datadog works by installing a lightweight Datadog Agent on the server or infrastructure. The Agent collects metrics, logs, events, and traces from the operating system and applications. It securely sends this data to the Datadog Backend, where it is processed and stored. Users can then create dashboards, configure alerts, run queries, analyze logs, and monitor application performance through the Datadog web interface.

