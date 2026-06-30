# APM Traces – Transactions, Basic Search, Search Pane, and Facets (Datadog)

These are the most commonly used features in **Datadog APM** for troubleshooting application performance issues. As a DevOps Engineer, you'll use them daily to investigate slow APIs, errors, and service performance.

---

# 1. APM Traces

## What is a Trace?

A **Trace** represents the **complete journey of a single request** as it travels through different services in your application.

A trace shows:

* Which services handled the request
* How much time each service took
* Where delays occurred
* Whether any errors happened

### Simple Definition

> A **Trace** is the complete path of one request from start to finish.

---

## Example

Suppose a user logs into your application.

```text
User

   │

   ▼

Login API

   │

   ▼

Authentication Service

   │

   ▼

Oracle Database

   │

   ▼

Response
```

This complete flow is called **one Trace**.

---

## Trace Details

Example:

```text
Trace ID : 8b12345

Service            Time

API Gateway        15 ms

Login Service      120 ms

Oracle Query       850 ms

Response           10 ms

----------------------------

Total Time         995 ms
```

Datadog immediately highlights that the **Oracle Query** is taking the most time.

---

# What Information Does a Trace Contain?

A trace includes:

* Trace ID
* Service Name
* Operation Name
* Request Duration
* Start Time
* End Time
* Error Status
* Tags
* Host Name
* Environment (Dev/Test/Prod)

---

# Benefits of Traces

* Identify slow APIs
* Find slow database queries
* Detect service failures
* Troubleshoot distributed applications
* Perform root cause analysis

---

# 2. Transactions

## What is a Transaction?

A **Transaction** is a **business operation or user request** performed by the application.

Examples:

* User Login
* Create Order
* Payment
* Search Product
* Upload File
* Download Report

Each transaction generates one or more traces.

---

## Example

```text
Customer clicks "Login"

↓

Login Transaction

↓

Authentication Service

↓

Oracle Database

↓

Login Successful
```

Here, **Login** is the transaction.

---

## Common Transactions

| Transaction       | Description              |
| ----------------- | ------------------------ |
| Login             | User authentication      |
| Create Order      | Customer places an order |
| Payment           | Payment processing       |
| Search Product    | Product search request   |
| User Registration | Create a new user        |
| Upload Document   | Upload a file            |

---

## Why Monitor Transactions?

To answer questions like:

* Which transaction is slow?
* Which transaction fails the most?
* Which transaction has the highest response time?
* Which transaction is generating errors?

---

# 3. Basic Search

Datadog APM provides a **search bar** to quickly find traces.

You can search using:

* Service Name
* Resource Name
* Environment
* Host
* Status
* Duration
* HTTP Method
* Tags

---

## Examples

Search by service:

```text
service:login-service
```

Search by environment:

```text
env:production
```

Search by status:

```text
status:error
```

Search by host:

```text
host:web-server-01
```

Search by duration:

```text
duration:>2s
```

Search by HTTP method:

```text
http.method:POST
```

Search by endpoint:

```text
resource_name:/login
```

---

## Combined Search

```text
service:payment-service
env:production
status:error
duration:>5s
```

This displays only traces matching all these conditions.

---

# 4. Search Pane

The **Search Pane** is the filtering area in Datadog APM.

It helps narrow down traces quickly.

Typical filters include:

* Service
* Environment
* Version
* Host
* Resource
* HTTP Status Code
* Duration
* Error
* Operation Name
* Tags

---

## Example

```text
Search Pane

Service

✓ login-service

Environment

✓ Production

Status

✓ Error

Duration

> 2 seconds

Host

web-server-01
```

Datadog updates the trace list immediately.

---

# Benefits of Search Pane

* Quickly isolate production issues
* Filter slow traces
* Find failed requests
* Analyze one specific service
* Reduce troubleshooting time

---

# 5. Facets

## What are Facets?

A **Facet** is an indexed attribute used for filtering, grouping, and analyzing traces.

Think of a facet as a searchable property.

---

## Common Facets

| Facet                | Example         |
| -------------------- | --------------- |
| Service              | login-service   |
| Environment          | production      |
| Host                 | server-01       |
| Version              | 2.3.1           |
| HTTP Method          | POST            |
| Status Code          | 500             |
| Region               | us-east-1       |
| Availability Zone    | us-east-1a      |
| Kubernetes Namespace | production      |
| Container Name       | login-container |

---

## Example

Suppose you have:

```text
5000 Traces
```

Using the facet:

```text
Environment

↓

Production
```

Results:

```text
1200 Traces
```

Now select:

```text
Status

↓

Error
```

Results:

```text
75 Traces
```

Now select:

```text
Service

↓

Payment Service
```

Results:

```text
8 Traces
```

Instead of checking all 5000 traces, you now focus on only the relevant 8 traces.

---

# Search vs Facets

| Basic Search                            | Facets                                             |
| --------------------------------------- | -------------------------------------------------- |
| Uses search queries                     | Uses predefined filters                            |
| Flexible                                | Quick filtering                                    |
| Good for advanced searches              | Good for interactive analysis                      |
| Example: `service:web-api status:error` | Click **Service → web-api** and **Status → Error** |

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

Cloud Spanner

      │

      ▼

Migration Application

      │

      ▼

Datadog APM
```

Suppose the migration API is slow.

### Search:

```text
service:migration-api
```

Then filter:

```text
status:error
```

Then filter:

```text
duration:>5s
```

Finally, use facets:

* Environment → Production
* Host → migration-vm-01
* Resource → /migrate
* Database → Oracle

Datadog displays only the slow, failed migration requests.

---

# End-to-End Flow

```text
User Request

      │

      ▼

Migration API

      │

      ▼

Striim

      │

      ▼

Oracle Database

      │

      ▼

Datadog Trace

      │

      ▼

Search

      │

      ▼

Search Pane Filters

      │

      ▼

Facets

      │

      ▼

Root Cause Analysis
```

---

# Interview Questions

### Q1. What is a Trace?

**Answer:**

A trace is the complete end-to-end journey of a single request through one or more services. It helps identify latency, errors, and bottlenecks across distributed applications.

---

### Q2. What is a Transaction in Datadog APM?

**Answer:**

A transaction represents a business operation or user request, such as login, payment, or order creation. Each transaction generates one or more traces that can be analyzed for performance and errors.

---

### Q3. What is the Search Pane?

**Answer:**

The Search Pane provides filters such as service, environment, host, status, duration, and tags to quickly narrow down traces and investigate application issues.

---

### Q4. What are Facets?

**Answer:**

Facets are indexed attributes in Datadog APM used to filter, group, and analyze traces. Common facets include service, environment, host, version, HTTP method, status code, and region, making it easier to locate specific trace data.

---

## DevOps Perspective

As a **DevOps Engineer**, you use these APM features to:

* Investigate slow API responses after deployments.
* Identify which transaction or service is causing latency.
* Search production traces for specific errors.
* Filter traces using the Search Pane during incident troubleshooting.
* Use facets to narrow down issues by environment, host, service, or version.
* Reduce Mean Time to Resolution (MTTR) by quickly identifying the root cause of application performance problems.
