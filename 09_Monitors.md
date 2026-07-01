# Datadog Monitors

## What is a Monitor?

A **Monitor** in Datadog is a feature that continuously watches your infrastructure, applications, logs, metrics, and services. When a defined condition (threshold) is met, Datadog automatically generates an alert and sends a notification to the appropriate team.

### Simple Definition

> **A Monitor is an automated alert that continuously checks the health and performance of your infrastructure and applications.**

---

# Why Do We Need Monitors?

Imagine you have a production application.

Without monitors:

* Users report the application is down.
* DevOps team manually checks logs and servers.
* Problem is detected late.

With monitors:

* Datadog detects the issue automatically.
* An alert is sent immediately.
* DevOps team starts troubleshooting before users are heavily impacted.

---

# How Monitors Work

```text
                Infrastructure / Application
                           │
                           ▼
                  Datadog Agent Collects Data
                           │
                           ▼
                    Datadog Backend
                           │
                 Monitor Evaluates Rules
                           │
           CPU > 90% ?  Error Rate > 5% ?
                           │
                     Yes → Alert Triggered
                           │
                           ▼
         Email / Slack / Teams / PagerDuty
```

---

# Monitor Workflow

```text
Application Running
        │
        ▼
Datadog Collects Metrics
        │
        ▼
Monitor Checks Condition
        │
        ▼
Condition Met?
      │
 ┌────┴─────┐
 │          │
No         Yes
 │          │
 ▼          ▼
Continue   Generate Alert
            │
            ▼
 Notify DevOps Team
```

---

# Types of Monitors

The screen you shared shows several monitor types.

## 1. Host Monitor

Monitors the health of servers or virtual machines.

Monitors:

* CPU
* Memory
* Disk
* Network
* Host Availability

Example:

```text
Host CPU > 90%

↓

Alert
```

---

## 2. Metric Monitor

Monitors any metric collected by Datadog.

Examples:

* CPU Usage
* Memory Usage
* Network Traffic
* Disk Usage
* Request Count

Example:

```text
Memory Usage > 80%

↓

Alert
```

---

## 3. Anomaly Monitor

Detects unusual behavior automatically using machine learning.

Example:

Normally:

```text
CPU = 35%
```

Today:

```text
CPU = 95%
```

Datadog recognizes this as an anomaly and generates an alert.

---

## 4. APM Monitor

Monitors application performance.

Examples:

* API Response Time
* Request Latency
* Error Rate
* Throughput

Example:

```text
Login API

Response Time > 3 seconds

↓

Alert
```

---

## 5. Audit Logs Monitor

Monitors audit log events.

Examples:

* User Login
* Permission Changes
* Configuration Updates
* API Key Creation

Example:

```text
Admin Permission Changed

↓

Alert
```

---

## 6. Composite Monitor

Combines multiple monitors into one.

Example:

```text
CPU > 90%

AND

Memory > 85%

↓

Alert
```

This reduces unnecessary alerts.

---

## 7. Custom Check Monitor

Monitors custom scripts written by your organization.

Example:

```text
Custom Script

↓

Checks Oracle Listener

↓

Alert if Down
```

---

## 8. Event Monitor

Monitors system events.

Examples:

* Deployment Completed
* Service Restarted
* Kubernetes Pod Deleted
* Jenkins Job Failed

---

## 9. Forecast Monitor

Predicts future problems.

Example:

```text
Disk Usage

Today = 80%

Tomorrow = 92%

↓

Alert Before Disk is Full
```

---

## 10. Integration Monitor

Monitors integrated services.

Examples:

* Oracle
* MySQL
* AWS
* Azure
* GCP
* Kubernetes

---

## 11. Live Process Monitor

Monitors running processes.

Example:

```text
Java Process

↓

Stopped

↓

Alert
```

---

# Example: CPU Monitor

Condition:

```text
CPU Usage > 90%

for 5 Minutes
```

Workflow:

```text
Server

↓

CPU = 95%

↓

Datadog Monitor

↓

Alert

↓

Slack + Email
```

---

# Example: APM Monitor

Condition:

```text
Payment API

Response Time > 2 Seconds
```

Workflow:

```text
Customer

↓

Payment API

↓

Response Time = 4 Seconds

↓

Datadog APM Monitor

↓

Alert
```

---

# Example: Database Monitor

```text
Oracle Connections

>

500

↓

Alert
```

---

# Real Project Example (Your Data Migration Project)

Your project:

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
Datadog
```

Possible monitors:

| Component        | Monitor                       |
| ---------------- | ----------------------------- |
| Oracle Database  | CPU, Sessions, Slow Queries   |
| Striim           | Process Running, Memory Usage |
| Cloud Spanner    | Latency, Error Rate           |
| Migration API    | Response Time                 |
| GCP VM           | CPU, Memory, Disk             |
| Application Logs | Error Monitor                 |

---

# Alert Notification Flow

```text
Application

↓

Datadog Agent

↓

Datadog Backend

↓

Monitor Evaluates

↓

Threshold Crossed

↓

Alert Created

↓

Slack

Email

PagerDuty

Microsoft Teams
```

---

# Best Practices

* Set realistic thresholds (avoid alert fatigue).
* Use warning and critical thresholds.
* Add meaningful monitor names and descriptions.
* Configure notifications to the correct team.
* Test monitors before using them in production.
* Review and tune monitors regularly.

---

# Interview Questions

## Q1. What is a Monitor in Datadog?

**Answer:**

A Monitor is a Datadog feature that continuously evaluates metrics, logs, traces, events, or service health against defined conditions. If a condition is met, Datadog automatically generates an alert and sends notifications through channels such as Email, Slack, Microsoft Teams, or PagerDuty.

---

## Q2. What are the common types of Monitors?

Common monitor types include:

* Host Monitor
* Metric Monitor
* APM Monitor
* Log Monitor
* Anomaly Monitor
* Composite Monitor
* Event Monitor
* Forecast Monitor
* Integration Monitor
* Live Process Monitor
* Custom Check Monitor

---

## Q3. How are Monitors used in a DevOps project?

In a DevOps project, monitors are configured to track infrastructure health, application performance, databases, Kubernetes clusters, CI/CD pipelines, and cloud services. They automatically notify the operations team when thresholds are exceeded or failures occur, enabling faster incident response and reducing downtime.

---

## DevOps Perspective (Your Project)

For your **Oracle → Striim → Cloud Spanner** migration project, you would typically create monitors for:

* **Oracle Database:** High CPU, connection count, slow queries.
* **Striim:** Process status, pipeline lag, memory usage.
* **Cloud Spanner:** High latency, failed transactions, CPU utilization.
* **Migration API:** Response time, error rate, throughput.
* **GCP VM:** CPU, memory, disk space, network usage.
* **Logs:** Failed migration jobs or application exceptions.

These monitors help ensure the migration pipeline remains healthy and alert the DevOps team immediately if any component experiences issues.

---
Below are **small notes** explaining **when to use each monitor** from a DevOps perspective.

| **Monitor Type**         | **When to Use**                                                              | **Example**                                                        |
| ------------------------ | ---------------------------------------------------------------------------- | ------------------------------------------------------------------ |
| **Host Monitor**         | Monitor the health of a server or VM.                                        | Alert if CPU > 90% or Memory > 85% on a Linux server.              |
| **Metric Monitor**       | Monitor any metric collected by Datadog.                                     | Alert if API response time > 2 sec or Disk usage > 80%.            |
| **Anomaly Monitor**      | Detect unusual behavior automatically using machine learning.                | CPU usually stays at 30%, suddenly jumps to 95%.                   |
| **APM Monitor**          | Monitor application performance and traces.                                  | Alert if Login API response time > 5 sec or Error rate > 5%.       |
| **Audit Logs Monitor**   | Monitor audit/security events.                                               | Alert when a user deletes a dashboard or changes monitor settings. |
| **Composite Monitor**    | Combine multiple monitor conditions into one alert.                          | Alert only if CPU > 90% **AND** Memory > 90%.                      |
| **Custom Check Monitor** | Monitor custom scripts or applications using Agent checks.                   | Custom script checks if Oracle listener is running.                |
| **Event Monitor**        | Monitor events generated by applications or cloud services.                  | Alert when a deployment starts or a Kubernetes node restarts.      |
| **Forecast Monitor**     | Predict future metric values before they become a problem.                   | Disk usage will reach 100% in the next 2 days.                     |
| **Integration Monitor**  | Monitor integrated services like AWS, GCP, Oracle, Kubernetes, Jenkins, etc. | Alert if Oracle database is down or GCP VM CPU is high.            |
| **Live Process Monitor** | Monitor running processes on servers.                                        | Alert if the Striim process or Java process stops unexpectedly.    |

---

# Real Project Example (Your Data Migration Project)

Your project:

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
```

| **Component**          | **Recommended Monitor** | **Reason**                                   |
| ---------------------- | ----------------------- | -------------------------------------------- |
| GCP VM                 | Host Monitor            | Monitor CPU, Memory, Disk, Network           |
| Migration API          | APM Monitor             | Monitor response time and errors             |
| Oracle Database        | Integration Monitor     | Monitor database health and connections      |
| Striim Process         | Live Process Monitor    | Detect if the Striim service stops           |
| Migration Latency      | Metric Monitor          | Monitor migration time or throughput         |
| Failed Deployment      | Event Monitor           | Alert on deployment events                   |
| Disk Filling Up        | Forecast Monitor        | Predict disk exhaustion before it happens    |
| High CPU + High Memory | Composite Monitor       | Alert only when both conditions occur        |
| Oracle Listener Check  | Custom Check Monitor    | Monitor a custom Oracle health check         |
| Unusual CPU Spike      | Anomaly Monitor         | Detect abnormal resource usage automatically |

---

# Quick Interview Summary

| **Monitor Type** | **One-Line Purpose**                              |
| ---------------- | ------------------------------------------------- |
| **Host**         | Monitor server health.                            |
| **Metric**       | Monitor any collected metric.                     |
| **Anomaly**      | Detect unusual behavior automatically.            |
| **APM**          | Monitor application performance and traces.       |
| **Audit Logs**   | Monitor security and audit activities.            |
| **Composite**    | Combine multiple monitor conditions.              |
| **Custom Check** | Monitor custom scripts or application checks.     |
| **Event**        | Monitor deployment and system events.             |
| **Forecast**     | Predict future resource issues.                   |
| **Integration**  | Monitor third-party services and cloud resources. |
| **Live Process** | Monitor whether important processes are running.  |

These are the monitor types you'll most commonly use in production as a DevOps engineer to proactively detect infrastructure, application, and service issues.
