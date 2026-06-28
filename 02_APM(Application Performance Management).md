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

## DevOps Perspective

As a **DevOps Engineer**, you typically use Datadog APM to:

* Monitor application performance after deployments.
* Detect performance regressions introduced by new releases.
* Correlate application traces with infrastructure metrics and logs.
* Troubleshoot production issues faster using distributed tracing.
* Create alerts for high latency, increased error rates, or low throughput.
* Verify that applications remain healthy after CI/CD deployments (e.g., through Harness).
* Share performance dashboards with development teams to improve application reliability.
