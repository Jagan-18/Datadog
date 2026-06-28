# Host, Datadog Agent, Datadog tags:

## What is a host?

A host is any physical or virtual OS instance that you monitor with Datadog. It could be a server, VM, node (in the case of Kubernetes) or App Service Plan instance (in the case of Azure App Services). In simple words this is your server where Datadog agent is installed.

---
## What is a Datadog Agent?

The Datadog Agent is software that runs on your hosts. It collects events and metrics from hosts and sends them to Datadog, where you can analyze your monitoring and performance data.

Datadog Agent is the **heart** of Datadog.

The Datadog Agent acts like a middle layer between your application and Datadog website.

The Datadog Agent collects metric and events from your systems and apps.

---
## What are Datadog tags?

Tags are a way of adding dimensions to Datadog telemetries so they can be filtered, aggregated, and compared in Datadog visualizations. Using tags enables you to observe aggregate performance across several hosts.

**Example:** `version: stage`, `version: prod`

---
# 1. What is a Host?

## Definition

A **Host** is any machine (physical server, virtual machine, cloud instance, or Kubernetes node) that runs an operating system and applications.

In Datadog, a **Host** is any machine being monitored by the Datadog Agent.

> **Simple Definition:**
> A **Host** is the machine where your application is running and where the Datadog Agent is installed.

---

## Host Examples

A Host can be:

* Physical Server
* Linux Server
* Windows Server
* GCP VM
* AWS EC2 Instance
* Azure VM
* Kubernetes Node
* Virtual Machine

---

## Architecture

```text
               Datadog Backend
                     ▲
                     │
              Datadog Agent
                     ▲
                     │
        +-------------------------+
        |      Linux Server       |
        |-------------------------|
        | Java Application        |
        | Oracle Database         |
        | Operating System        |
        +-------------------------+

This Linux Server is called a HOST.
```

---

## Real Example

Suppose your company has:

```text
Host-1 → Oracle Database Server

Host-2 → Striim Server

Host-3 → Application Server

Host-4 → Cloud Spanner Connector
```

Each machine is a **Host**.

The Datadog Agent is installed on each host.

---

## Host Information Collected

Datadog collects:

* Host Name
* CPU Usage
* Memory Usage
* Disk Usage
* Network Usage
* Running Processes
* Installed Services
* Operating System

---

## Interview Answer

**Q. What is a Host?**

> A Host is any physical server, virtual machine, cloud instance, or Kubernetes node that runs applications. In Datadog, a Host is a machine monitored by the Datadog Agent.

---

# 2. What is Datadog Agent?

## Definition

The **Datadog Agent** is a lightweight software installed on a Host.

Its job is to collect monitoring data and send it securely to the Datadog Backend.

---

## Simple Definition

> The Datadog Agent is a lightweight software that collects metrics, logs, traces, and events from a Host and sends them to the Datadog Cloud.

---

## Architecture

```text
           Datadog Backend
                 ▲
                 │ HTTPS
                 │
          Datadog Agent
                 ▲
                 │
             Linux Server
```

---

## What Does the Agent Collect?

* CPU Usage
* Memory Usage
* Disk Usage
* Network Usage
* Application Metrics
* Database Metrics
* Application Logs
* System Logs
* APM Traces
* Process Information

---

## Data Collection Flow

```text
Application

      │

Operating System

      │

Datadog Agent

      │

HTTPS

      │

Datadog Backend

      │

Dashboard
```

---

## Real Project Example

Your project:

```text
Oracle

   │

Striim

   │

Cloud Spanner

   │

Migration Application

   │

GCP VM (Host)

   │

Datadog Agent

   │

Datadog Backend
```

The Agent collects:

* Oracle metrics
* Striim metrics
* Cloud VM CPU
* Memory
* Logs
* Network
* Disk

---

## Interview Answer

**Q. What is Datadog Agent?**

> Datadog Agent is a lightweight software installed on a Host. It collects infrastructure metrics, application metrics, logs, traces, and events, then securely sends them to the Datadog Backend for monitoring and alerting.

---

# 3. What are Datadog Tags?

## Definition

**Tags** are **key-value labels** attached to Hosts, applications, services, containers, or cloud resources.

They help organize, filter, search, and group monitoring data.

---

## Simple Definition

> Tags are labels used to identify and categorize resources in Datadog.

---

## Syntax

```text
key:value
```

Examples:

```text
env:prod

env:dev

team:devops

application:payment

region:us-east1
```

---

## Why Do We Use Tags?

Without tags:

```text
100 Servers
```

It is difficult to identify which server belongs to which environment or team.

With tags:

```text
Server-01

env:prod

team:devops

application:payment
```

Now you can easily filter and search.

---

## Example

```text
Host-01

env:prod

team:datafactory

application:striim

region:india
```

---

## Architecture

```text
                 Host

            Linux Server

                 │

        Datadog Agent

                 │

Tags

env:prod

team:devops

application:payment

                 │

Datadog Backend

                 │

Dashboard Filter
```

---

## Common Tags

| Tag         | Example                     |
| ----------- | --------------------------- |
| Environment | env:dev, env:test, env:prod |
| Team        | team:devops                 |
| Application | application:striim          |
| Service     | service:oracle              |
| Region      | region:asia-south1          |
| Cloud       | cloud:gcp                   |
| Project     | project:data-migration      |
| Version     | version:v1.0                |

---

## Benefits of Tags

* Organize resources
* Filter dashboards
* Search hosts
* Create alerts
* Group metrics
* Generate reports
* Separate Dev, Test, and Prod environments

---

## Real Project Example

Your project uses:

* Oracle
* Striim
* Cloud Spanner
* GCP
* Datadog

Example tags:

```text
env:prod

project:data-migration

team:devops

application:striim

database:oracle

cloud:gcp
```

Now you can quickly filter dashboards or alerts for only the production data migration resources.

---

# Difference Between Host, Agent, and Tags

| Feature     | Host                       | Datadog Agent                  | Tags                                  |
| ----------- | -------------------------- | ------------------------------ | ------------------------------------- |
| What is it? | A machine (server/VM/node) | Software installed on the Host | Labels used to categorize resources   |
| Purpose     | Runs applications          | Collects monitoring data       | Organizes and filters monitoring data |
| Installed?  | No                         | Yes                            | No (configured as metadata)           |
| Example     | GCP VM                     | Datadog Agent                  | env:prod, team:devops                 |

---

# Interview Questions

### Q1. What is a Host?

> A Host is a physical server, virtual machine, cloud instance, or Kubernetes node that runs applications and is monitored by Datadog.

### Q2. What is Datadog Agent?

> The Datadog Agent is a lightweight software installed on a Host. It collects metrics, logs, traces, and events and sends them securely to the Datadog Backend.

### Q3. What are Datadog Tags?

> Datadog Tags are key-value labels used to identify, organize, search, filter, and group monitored resources such as hosts, applications, containers, and cloud services.

---

## Easy Way to Remember

```text
Host
│
│  (Machine)
▼
Datadog Agent
│
│  (Collects Data)
▼
Datadog Backend
│
│  (Stores & Displays Data)
▼
Dashboard

Tags = Labels used to organize and filter the data.
```

### One-line summary

* **Host** = The machine being monitored.
* **Datadog Agent** = The software that collects monitoring data from the Host.
* **Tags** = Labels that help organize, filter, and search monitoring data.
