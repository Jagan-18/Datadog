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
> The **Datadog Agent** is a lightweight software installed on hosts such as VMs, servers, containers, or Kubernetes nodes. It collects metrics, logs, traces, and system information and securely sends them to the Datadog Backend. The **Datadog Backend** is the cloud-based SaaS platform that receives, stores, analyzes, and visualizes this data. It provides dashboards, alerting, log management, APM, and analytics, enabling DevOps teams to monitor and troubleshoot their infrastructure and applications from a centralized platform.
