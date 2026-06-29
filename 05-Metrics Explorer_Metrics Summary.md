Metrics can be submitted in 3 ways:
1. Agent 
2. DogStatsId (which comes with the Agent)
3. Datadog HTTP’s API

# Metric Types:
Datadog Agent performs the following actions:
1. Collects data in specific time interval
2. Aggregate this data
3. Send this data to Datadog and it will be presented as single point in the graph

#### Depends how those Aggregation is done we have different Metric Types.

**1. COUNT**  - This host emits the following values in a flush time interval: [1,1,1,2,2,2,3,3]. Agent will submit single data point with 15 as a value.

**2. RATE** - This host emits the following values in a flush time interval: [1,1,1,2,2,2,3,3]. Agent will submit single data point with 1.5 as value.

**3. GAUGE** - This host emits the following values in a flush time interval: [71,71,71,71,71,71,71.5]. Agent will submit single data point with 71.5 as value.

**4. DISTRUBUTION** - The DISTRIBUTION metric submission type represents the global statistical distribution of a set of values calculated across your entire distributed infrastructure in one time interval. 

---
# Metrics Explorer

**Metrics Explorer** is a Datadog feature used to **view, search, filter, analyze, and visualize infrastructure and application metrics in real time**.

It helps you understand the health and performance of your systems by displaying metrics in graphs and charts.

---

# What is Metrics Explorer?

Metrics Explorer is a built-in Datadog tool that allows you to:

* View real-time metrics
* Search for any available metric
* Filter metrics using tags
* Group metrics by hosts, services, or regions
* Create graphs and dashboards
* Analyze historical metric data

---

# Why do we use Metrics Explorer?

Suppose your production server is running slowly.

You want to check:

* CPU Usage
* Memory Usage
* Disk Usage
* Network Traffic

Instead of logging into the server, you simply open **Metrics Explorer**.

Example:

```text
Datadog

↓

Metrics Explorer

↓

system.cpu.user

↓

Graph Displayed
```

---

# Architecture

```text
                Linux Server
                      │
                Datadog Agent
                      │
                Collects Metrics
                      │
                      ▼
               Datadog Backend
                      │
              Metrics Database
                      │
                      ▼
             Metrics Explorer
                      │
          Graphs & Visualizations
```

---

# What can you do in Metrics Explorer?

### 1. Search Metrics

Example:

```text
Search

system.cpu.user
```

Result:

```text
CPU Usage Graph
```

---

### 2. Filter Metrics

Example:

```text
env:prod

team:devops

application:payment
```

Only production metrics are displayed.

---

### 3. Group Metrics

Example

Group by:

* Host
* Region
* Availability Zone
* Kubernetes Node

```text
CPU Usage

Host-1

Host-2

Host-3
```

---

### 4. Aggregate Metrics

Supported aggregation methods:

* Average (avg)
* Sum
* Minimum (min)
* Maximum (max)
* Count

Example:

```text
Average CPU Usage

Host1 = 40%

Host2 = 60%

Average = 50%
```

---

### 5. Change Time Range

You can analyze data for:

* Last 15 Minutes
* Last 1 Hour
* Last 4 Hours
* Today
* Yesterday
* Last 7 Days
* Last 30 Days

Example

```text
Time Range

Last 1 Hour
```

---

# Common Metrics

| Metric Name           | Description      |
| --------------------- | ---------------- |
| system.cpu.user       | CPU Usage        |
| system.mem.used       | Used Memory      |
| system.mem.free       | Free Memory      |
| system.disk.used      | Disk Usage       |
| system.disk.free      | Free Disk Space  |
| system.net.bytes_rcvd | Network Received |
| system.net.bytes_sent | Network Sent     |
| system.load.1         | System Load      |
| system.uptime         | Host Uptime      |

---

# Example

Suppose CPU usage suddenly increases.

Search:

```text
system.cpu.user
```

Graph:

```text
CPU %

100 ────────────────

 80 ────────▲───────

 60 ───────▲────────

 40 ─────▲──────────

 20 ───▲────────────

  0─────────────────

     Time
```

---

# Filter Example

You have:

```text
100 Servers
```

Filter:

```text
env:prod
```

Result:

```text
25 Production Servers
```

---

# Group By Example

```text
Group By

Host
```

Result:

```text
Host-1

CPU = 40%

Host-2

CPU = 65%

Host-3

CPU = 80%
```

---

# Real Project Example (Your Data Migration Project)

Your project uses:

* Oracle
* Cloud Spanner
* Striim
* GCP
* Datadog

You can monitor metrics such as:

```text
Oracle CPU

Oracle Sessions

GCP VM CPU

Memory Usage

Disk Usage

Network Traffic

Striim Process Metrics
```

Metrics Explorer displays all these metrics in one place.

---

# Data Flow

```text
Oracle Database
       │
       ▼
GCP VM (Host)
       │
       ▼
Datadog Agent
       │
       ▼
Datadog Backend
       │
       ▼
Metrics Explorer
       │
       ▼
Graphs
Filters
Aggregations
Dashboards
```

---

# Benefits of Metrics Explorer

* Real-time monitoring
* Search any metric
* Filter using tags
* Group by hosts or services
* Historical analysis
* Easy graph creation
* Dashboard integration
* Troubleshoot performance issues quickly

---
### Q. What is Metrics Explorer in Datadog?

**Answer:**

> Metrics Explorer is a Datadog feature that allows users to search, visualize, filter, and analyze infrastructure and application metrics in real time. It supports metric aggregation, grouping by tags, historical data analysis, and graph creation. It helps DevOps and operations teams monitor system health, troubleshoot issues, and build dashboards for infrastructure and application performance monitoring.

---
# Metrics Summary

## What is a Metric?

A **metric** is a numerical measurement collected over time that represents the health, performance, or behavior of a system, application, database, or network.

### Simple Definition

> **A metric is a numeric value that tells us how a resource is performing at a specific point in time.**

Examples:

* CPU Usage = 65%
* Memory Usage = 70%
* Disk Usage = 80%
* API Response Time = 250 ms
* Network Traffic = 150 Mbps

---

# What is Metrics Summary?

**Metrics Summary** is a Datadog feature that provides an overview of all the metrics collected in your Datadog account. It allows you to search, view, and understand information about each metric.

Metrics Summary helps you answer questions like:

* What metrics are available?
* Which hosts are sending a metric?
* What tags are associated with a metric?
* What type of metric is it?
* How often is the metric reported?

---

## What information does Metrics Summary provide?

For each metric, you can see:

* Metric Name
* Metric Type
* Description
* Unit
* Hosts reporting the metric
* Associated Tags
* Source (Agent, Integration, Custom)
* Last Reported Time
* Number of Hosts
* Usage Information

---

## Example

Suppose you search for:

```text
system.cpu.user
```

Metrics Summary displays:

```text
Metric Name      : system.cpu.user
Metric Type      : Gauge
Unit             : Percentage
Host             : gcp-prod-vm01
Tags             : env:prod, team:devops
Source           : Datadog Agent
Last Reported    : 10 seconds ago
```

---

# Architecture

```text
Linux Server
      │
      ▼
Datadog Agent
      │
Collects Metrics
      │
      ▼
Datadog Backend
      │
      ▼
Metrics Summary
```

---

# Benefits of Metrics Summary

* View all available metrics
* Understand metric types
* Verify metrics are being collected
* Identify metric sources
* Check reporting hosts
* Troubleshoot missing metrics
* Discover custom metrics

---

# Metric Types in Datadog

Datadog supports several metric types.

The most common are:

1. Gauge
2. Count
3. Rate
4. Histogram
5. Distribution
6. Set

---

# 1. Gauge

A **Gauge** represents the **current value** of a metric.

It can increase or decrease.

### Examples

* CPU Usage
* Memory Usage
* Disk Usage
* Temperature

Example

```text
Time      CPU%

10:00      40

10:05      55

10:10      35

10:15      70
```

The latest value is always important.

**Common Metrics**

```text
system.cpu.user

system.mem.used

system.disk.used
```

---

# 2. Count

A **Count** measures **how many times an event occurred** during a time interval.

### Examples

* Number of Requests
* Number of Errors
* Number of Logins
* Number of Transactions

Example

```text
1 Minute

Login Requests

250
```

Every minute the counter increases based on events.

**Common Metrics**

```text
http.requests

application.errors
```

---

# 3. Rate

A **Rate** measures **how fast something happens over time**.

Formula

```text
Rate = Count / Time
```

### Examples

* Requests per Second
* Bytes per Second
* Errors per Minute

Example

```text
600 Requests

1 Minute

Rate = 10 Requests/sec
```

---

# 4. Histogram

A **Histogram** measures the **distribution of values** and automatically calculates statistics.

It provides:

* Count
* Average
* Minimum
* Maximum
* Median
* 95th Percentile (P95)
* 99th Percentile (P99)

### Example

API Response Times

```text
120 ms

140 ms

150 ms

400 ms

900 ms
```

Histogram calculates:

```text
Average = 342 ms

Min = 120 ms

Max = 900 ms

P95 = 850 ms
```

Used for:

* API Response Time
* Database Query Time
* Latency

---

# 5. Distribution

A **Distribution** is similar to a Histogram but aggregates data **across all hosts globally** before calculating statistics.

### Example

Three servers report response times:

```text
Host1 = 120 ms

Host2 = 300 ms

Host3 = 800 ms
```

Datadog combines all values and calculates global percentiles.

Used for:

* Multi-host latency
* Global application performance
* Cloud-wide response time analysis

---

# 6. Set

A **Set** stores **unique values**.

Duplicate values are counted only once.

### Example

User IDs

```text
1001

1002

1002

1003

1001
```

Stored values:

```text
1001

1002

1003
```

Unique Count = 3

Used for:

* Unique Users
* Unique Sessions
* Unique IP Addresses

---

# Metric Types Comparison

| Metric Type  | Measures                         | Example            |
| ------------ | -------------------------------- | ------------------ |
| Gauge        | Current value                    | CPU = 65%          |
| Count        | Total number of events           | 500 Requests       |
| Rate         | Events per unit time             | 50 Requests/sec    |
| Histogram    | Distribution with statistics     | API response time  |
| Distribution | Global distribution across hosts | Multi-host latency |
| Set          | Unique values                    | Unique User IDs    |

---

# Real Project Example (Your Data Migration Project)

Suppose your migration environment has:

* Oracle Database
* Striim
* Cloud Spanner
* GCP VM

Example metrics:

| Component     | Metric             | Type         |
| ------------- | ------------------ | ------------ |
| GCP VM        | CPU Usage          | Gauge        |
| Oracle        | Active Sessions    | Gauge        |
| Striim        | Events Processed   | Count        |
| Migration API | Requests/sec       | Rate         |
| Cloud Spanner | Query Latency      | Histogram    |
| Multiple VMs  | Global API Latency | Distribution |
| User Sessions | Unique Session IDs | Set          |

---

# Data Flow

```text
Oracle
     │
Striim
     │
Migration App
     │
Datadog Agent
     │
Datadog Backend
     │
Metrics Summary
     │
Gauge
Count
Rate
Histogram
Distribution
Set
```

---
## Q1. What is Metrics Summary?

**Answer:**

> Metrics Summary is a Datadog feature that provides a centralized view of all collected metrics. It displays information such as the metric name, type, unit, tags, reporting hosts, source, and usage, making it easier to discover, understand, and troubleshoot metrics.

---

## Q2. What are the different metric types in Datadog?

**Answer:**

Datadog supports several metric types:

* **Gauge** – Current value (CPU, Memory)
* **Count** – Number of events
* **Rate** – Events per unit time
* **Histogram** – Distribution of values with statistics like min, max, average, and percentiles
* **Distribution** – Global distribution of values across multiple hosts
* **Set** – Unique values only

These metric types help monitor infrastructure, applications, databases, and cloud environments effectively.
