# APM (Application Performance Monitoring)

> **Note:** Although many people say **Application Performance Management**, Datadog officially uses the term **Application Performance Monitoring (APM)**. The purpose is the same: monitor and improve application performance.

---

# What is APM?

**Application Performance Monitoring (APM)** is a monitoring technique used to measure, analyze, and troubleshoot the performance, availability, and reliability of applications in real time.

It helps DevOps and developers quickly identify where performance problems occur in an application.

### Simple Definition

> **APM is used to monitor how well an application performs, identify slow transactions, detect errors, and troubleshoot performance issues before they affect users.**

---

# Why do we need APM?

Imagine your application is running in production.

Customers complain:

* Website is slow.
* Login takes 10 seconds.
* Payment API is failing.
* Users receive 500 Internal Server Errors.

Without APM:

* Check server logs
* Check application logs
* Check database
* Check API response
* Takes hours to identify the issue

With APM:

Datadog immediately shows:

* Which API is slow
* Which database query is slow
* Which service is failing
* Exact response time
* Error details
* Root cause

---

# Architecture

```text
                   User
                    │
                    ▼
            Web Application
                    │
      ┌─────────────┼─────────────┐
      ▼             ▼             ▼
  Login API    Payment API    Order API
      │             │             │
      └─────────────┼─────────────┘
                    │
          Datadog APM Agent
                    │
        Collects Traces & Metrics
                    │
              HTTPS / TLS
                    │
                    ▼
             Datadog Backend
                    │
      ┌─────────────┼─────────────┐
      ▼             ▼             ▼
 Service Map   Trace View    Dashboards
```

---

# What does APM Monitor?

### 1. Response Time

Measures how long an API or application takes to respond.

Example

```text
Login API

Normal Response Time

200 ms

Today

2500 ms
```

Datadog immediately highlights the slowdown.

---

### 2. Request Throughput

Shows how many requests are handled every second.

Example

```text
Requests

10/sec

100/sec

500/sec
```

Useful for identifying traffic spikes.

---

### 3. Error Rate

Shows the percentage of failed requests.

Example

```text
1000 Requests

980 Success

20 Failed

Error Rate = 2%
```

---

### 4. Latency

Latency is the total time taken to process a request.

Example

```text
User clicks Login

↓

Application

↓

Database

↓

Response
```

Total Time = Latency

---

### 5. Slow Transactions

APM identifies slow requests.

Example

```text
Login API

Normal

200 ms

Today

5 Seconds
```

Datadog shows why it became slow.

---

### 6. Database Queries

APM monitors database performance.

Example

```text
SELECT *

FROM EMPLOYEE

Execution Time

5 Seconds
```

Datadog identifies the slow query.

---

### 7. External Services

Tracks communication with:

* Payment Gateway
* REST APIs
* Microservices
* Cloud Services

---

### 8. Exceptions

Monitors:

* Java Exceptions
* NullPointerException
* TimeoutException
* Database Errors

---

# APM Components

## Services

A service is an application or microservice.

Example

```text
User Service

Order Service

Payment Service

Notification Service
```

---

## Traces

A trace represents the complete journey of a user request.

Example

```text
User Login

↓

API Gateway

↓

Authentication Service

↓

Oracle Database

↓

Response
```

This complete journey is called a **Trace**.

---

## Spans

A span represents one individual operation within a trace.

Example

```text
Trace

↓

Login API

↓

Authentication

↓

Database Query

↓

Response
```

Each step is a **Span**.

---

# Trace Example

```text
Trace ID : 12345

User Request

│

├── API Gateway (20 ms)

├── Login Service (100 ms)

├── Oracle Query (350 ms)

└── Response (10 ms)

Total

480 ms
```

Datadog highlights the slowest span.

---

# Service Map

Datadog automatically creates a Service Map.

```text
User

│

▼

API Gateway

│

├── Login Service

├── Order Service

├── Payment Service

└── Notification Service
```

You can quickly identify which service is failing.

---

# Root Cause Analysis

Example

Customer says:

> Login is slow.

Datadog APM shows:

```text
Login API

↓

Authentication

↓

Oracle Query

↓

Execution Time

8 Seconds
```

Root Cause:

Oracle Database Query is slow.

---

# Real Project Example (Your Data Migration Project)

Suppose your migration application has:

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
```

Datadog APM monitors:

* Migration API response time
* Striim application performance
* Database query execution time
* Cloud Spanner latency
* Oracle latency
* API failures
* Exception details

If migration becomes slow, APM pinpoints the exact component causing the delay.

---

# Benefits of APM

* Detect slow APIs
* Identify bottlenecks
* Monitor response time
* Monitor request throughput
* Track error rates
* Analyze database queries
* Perform root cause analysis
* Improve application performance
* Reduce Mean Time to Resolution (MTTR)
* Increase application availability

---

# Difference Between Infrastructure Monitoring and APM

| Infrastructure Monitoring           | APM                              |
| ----------------------------------- | -------------------------------- |
| Monitors servers and infrastructure | Monitors application performance |
| CPU                                 | API response time                |
| Memory                              | Request latency                  |
| Disk                                | Transaction performance          |
| Network                             | Error rate                       |
| VM health                           | Slow database queries            |
| Kubernetes nodes                    | Service dependencies             |
| Operating system metrics            | End-to-end request tracing       |

---

# Interview Questions

### Q1. What is APM?

**Answer:**

> Application Performance Monitoring (APM) is a monitoring solution that tracks the performance, availability, and reliability of applications. It provides visibility into response time, latency, throughput, error rates, database queries, and distributed traces, enabling teams to identify and resolve performance issues quickly.

---

### Q2. What does Datadog APM monitor?

**Answer:**

Datadog APM monitors:

* Application response time
* Latency
* Request throughput
* Error rate
* Distributed traces
* Database queries
* Service dependencies
* Exceptions
* External API calls
* Root cause of application issues

---

### Q3. What is the difference between a Trace and a Span?

| Trace                         | Span                                                   |
| ----------------------------- | ------------------------------------------------------ |
| Complete journey of a request | One individual operation within the journey            |
| Contains multiple spans       | Smallest unit of work                                  |
| Example: User Login request   | Example: Database query, API call, authentication step |

---

# How is APM Monitoring Performed?

Application Performance Monitoring (APM) is performed by **instrumenting the application** so that performance data is collected while the application is running. This data is then sent to an APM platform (such as Datadog), where it is analyzed and displayed through dashboards, traces, and alerts.

# Step-by-Step Process of APM Monitoring

## Step 1: Application is Running

The application is deployed on a server, virtual machine, container, or Kubernetes cluster.

Example:

```text
                Users
                  │
                  ▼
         E-Commerce Application
                  │
         -----------------------
         │         │           │
         ▼         ▼           ▼
     Login API  Order API  Payment API
```

---

## Step 2: Install the Datadog Agent

Install the **Datadog Agent** on the server or Kubernetes node where the application is running.

Example:

```text
Linux Server
│
├── Java Application
├── Oracle Database
└── Datadog Agent
```

The Datadog Agent collects:

* System Metrics
* Application Metrics
* Logs
* Traces
* Events

---

## Step 3: Instrument the Application

To monitor application performance, the application must be instrumented with the **Datadog APM library (Tracer)**.

Each programming language has its own tracer.

| Programming Language | Datadog Tracer      |
| -------------------- | ------------------- |
| Java                 | dd-java-agent.jar   |
| Python               | ddtrace             |
| Node.js              | dd-trace            |
| .NET                 | Datadog .NET Tracer |
| Go                   | dd-trace-go         |
| PHP                  | dd-trace-php        |
| Ruby                 | ddtrace             |

Example (Java):

```text
Application

↓

dd-java-agent.jar

↓

Application Starts

↓

Tracing Enabled
```

The tracer automatically captures:

* HTTP Requests
* API Calls
* Database Queries
* Exceptions
* Response Time

---

## Step 4: User Sends a Request

Example:

```text
User

↓

Login API
```

The request enters the application.

---

## Step 5: Tracer Creates a Trace

As the request moves through the application, the tracer records each operation.

Example:

```text
Login Request

↓

Authentication

↓

Oracle Database

↓

Generate Token

↓

Return Response
```

This complete journey is called a **Trace**.

---

## Step 6: Trace is Divided into Spans

Each operation inside the trace becomes a **Span**.

Example:

```text
Trace

│

├── API Gateway (20 ms)

├── Authentication (40 ms)

├── Oracle Query (500 ms)

└── Response (15 ms)
```

Each line is an individual span.

---

## Step 7: Datadog Agent Collects the Trace

The tracer sends trace information to the Datadog Agent.

```text
Application

↓

Datadog Tracer

↓

Datadog Agent
```

---

## Step 8: Agent Sends Data to Datadog Backend

The Agent securely sends all collected information using HTTPS.

```text
Datadog Agent

↓

HTTPS / TLS

↓

Datadog Backend
```

---

## Step 9: Datadog Processes the Data

The backend:

* Stores traces
* Calculates latency
* Calculates throughput
* Calculates error rate
* Builds Service Maps
* Creates Flame Graphs
* Links traces with logs and infrastructure metrics

---

## Step 10: Display Results

The DevOps team can now view:

* Service Map
* Traces
* Spans
* API Response Time
* Error Rate
* Throughput
* Slow Database Queries
* Alerts

---

# Complete APM Flow

```text
                   User
                     │
                     ▼
             Sends HTTP Request
                     │
                     ▼
              Web Application
                     │
          Datadog APM Tracer
                     │
     Creates Traces and Spans
                     │
                     ▼
              Datadog Agent
                     │
             HTTPS / TLS
                     │
                     ▼
             Datadog Backend
                     │
     ┌─────────┬──────────┬──────────┐
     ▼         ▼          ▼
 Dashboards  Traces    Alerts
```

---

# Real Example

A customer logs in to an application.

```text
Customer

↓

Login API

↓

Authentication Service

↓

Oracle Database

↓

Generate JWT Token

↓

Response
```

Datadog records:

| Operation      | Time   |
| -------------- | ------ |
| Login API      | 20 ms  |
| Authentication | 40 ms  |
| Oracle Query   | 600 ms |
| JWT Generation | 10 ms  |
| Response       | 5 ms   |

Total Response Time:

```text
20 + 40 + 600 + 10 + 5

= 675 ms
```

Datadog immediately identifies the **Oracle Query (600 ms)** as the bottleneck.

---

# What Information Does APM Collect?

* Request Count
* Response Time
* Latency
* Throughput
* Error Rate
* Exceptions
* API Calls
* Database Queries
* SQL Execution Time
* External Service Calls
* Distributed Traces
* Service Dependencies

---

# DevOps Perspective

In your project:

* **Cloud:** GCP
* **Source Database:** Oracle
* **Target Database:** Cloud Spanner
* **Migration Tool:** Striim
* **Monitoring:** Datadog
* **CI/CD:** Harness

APM helps you monitor:

```text
Client
   │
   ▼
Migration Application
   │
   ├── Oracle Database
   ├── Striim
   ├── Cloud Spanner
   └── External APIs
         │
         ▼
Datadog APM
         │
         ▼
Dashboard + Alerts
```

If a migration job becomes slow, APM can show whether the delay is caused by:

* A slow Oracle query
* High Cloud Spanner latency
* A slow Striim processing step
* An external API timeout

This enables DevOps and development teams to identify the root cause much faster than checking logs manually.

---
**Q: How is APM Monitoring Performed?**

**Answer:**

> APM monitoring is performed by instrumenting an application with a language-specific APM tracer (such as the Datadog Java Agent or Python `ddtrace`). The tracer captures request flows, response times, database calls, external service calls, and exceptions, creating traces and spans for each transaction. These traces are sent to the Datadog Agent, which forwards them securely to the Datadog Backend. The backend analyzes the data and presents it through dashboards, distributed traces, service maps, flame graphs, and alerts, enabling teams to quickly identify performance bottlenecks and troubleshoot application issues.

