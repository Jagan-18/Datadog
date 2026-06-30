# APM Services and Service Map

## What is an APM Service?

### Definition

An **APM Service** is a logical representation of an application or a part of an application that performs a specific business function.

In Datadog, every application, microservice, API, or backend component that generates traces is identified as a **Service**.

> **Simple Definition:**
>
> An **APM Service** is an application or microservice that Datadog monitors for performance.

---

## Examples of APM Services

Suppose you have an e-commerce application.

```text
E-Commerce Application

├── Login Service
├── User Service
├── Product Service
├── Cart Service
├── Payment Service
├── Order Service
└── Notification Service
```

Each one is a separate **APM Service** in Datadog.

---

## Real Project Example (Your Project)

Suppose your Data Migration project has:

```text
Migration Application

├── Oracle Connector
├── Striim Service
├── Migration API
├── Validation Service
└── Cloud Spanner Connector
```

Datadog treats each component as an individual **Service**.

---

# What Information Does Datadog Show for a Service?

For every service, Datadog displays:

* Service Name
* Request Count
* Response Time (Latency)
* Error Rate
* Throughput (Requests/sec)
* Resource Usage
* Database Calls
* External API Calls
* Dependencies
* Traces
* Logs

Example:

```text
Service Name : Payment Service

Response Time : 180 ms

Requests/sec : 250

Error Rate : 0.5%

Availability : 99.99%
```

---

# What is a Service Map?

### Definition

A **Service Map** is a graphical representation of how different services communicate with each other.

It automatically discovers service dependencies using distributed tracing.

> **Simple Definition:**
>
> A **Service Map** shows which services talk to each other and how they are connected.

---

# Why Do We Need a Service Map?

Imagine your application contains 20 microservices.

Without a Service Map:

* Difficult to know which service calls another service.
* Difficult to identify where failures occur.
* Troubleshooting takes longer.

With a Service Map:

* See all service dependencies visually.
* Identify failing services quickly.
* Trace requests across services.
* Find bottlenecks.

---

# Service Map Example

```text
                 User
                   │
                   ▼
              API Gateway
                   │
      ┌────────────┼────────────┐
      ▼            ▼            ▼
 Login Service  Order Service  Product Service
      │            │
      ▼            ▼
 Oracle DB     Payment Service
                   │
                   ▼
            Notification Service
```

Datadog automatically creates this map.

---

# How Does Datadog Build a Service Map?

Datadog APM collects distributed traces.

Example:

```text
User Login

↓

API Gateway

↓

Login Service

↓

Oracle Database

↓

Response
```

Each request generates trace information.

Using these traces, Datadog automatically builds the Service Map.

---

# Service Map Shows

For every service, Datadog displays:

* Service Name
* Dependencies
* Incoming Requests
* Outgoing Requests
* Latency
* Error Rate
* Traffic Volume
* Service Health

---

# Example

Suppose users report that payments are failing.

Service Map:

```text
User

↓

API Gateway

↓

Payment Service

↓

Bank API

↓

Timeout
```

Datadog highlights:

```text
Payment Service

Status : Red

Latency : High

Errors : 25%
```

This immediately identifies the root cause.

---

# Service Health Colors

```text
Green   → Healthy

Yellow  → Warning

Red     → Critical

Gray    → No Data
```

---

# End-to-End Flow

```text
Customer
    │
    ▼
API Gateway
    │
    ▼
Application Services
    │
    ▼
Datadog APM
    │
    ▼
Service Map
    │
    ▼
Dashboard & Alerts
```

---

# Difference Between APM Service and Service Map

| APM Service                                | Service Map                                              |
| ------------------------------------------ | -------------------------------------------------------- |
| Represents one application or microservice | Shows how all services communicate                       |
| Displays metrics for one service           | Displays relationships between services                  |
| Shows latency, throughput, and errors      | Shows dependencies and request flow                      |
| Used to monitor a single service           | Used to understand the complete application architecture |

---

# Real-Time Example (Your Project)

Your project architecture:

```text
Oracle Database
        │
        ▼
      Striim
        │
        ▼
Migration Service
        │
        ▼
Cloud Spanner
```

### APM Services

* Striim Service
* Migration Service
* Oracle Database
* Cloud Spanner

### Service Map

```text
Oracle Database
        │
        ▼
   Striim Service
        │
        ▼
 Migration Service
        │
        ▼
 Cloud Spanner
```

If the migration becomes slow, Datadog shows:

* Which service is slow.
* Where the request is delayed.
* Which dependency is causing the issue.
* End-to-end trace of the request.

---
### Q1. What is an APM Service?

**Answer:**

> An APM Service is a logical representation of an application, API, or microservice monitored by Datadog. It provides performance metrics such as request rate, latency, error rate, throughput, traces, and dependencies, helping teams monitor and troubleshoot application performance.

---

### Q2. What is a Service Map?

**Answer:**

> A Service Map is an automatically generated visual representation of service-to-service communication. It uses distributed tracing to show dependencies, traffic flow, latency, and error rates between services, making it easier to identify bottlenecks and troubleshoot issues.

---

### Q3. How is a Service Map created?

**Answer:**

> Datadog creates a Service Map automatically by analyzing distributed traces collected through Datadog APM. As requests flow between services, Datadog identifies their relationships and displays them in a graphical map along with performance and health information.
