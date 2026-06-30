# APM Traces – Error Tracing (Datadog)

## What is Error Tracing?

**Error Tracing** in Datadog APM helps identify, track, and analyze errors that occur while processing application requests. It allows developers and DevOps engineers to quickly find the **root cause** of failures by showing exactly **where**, **when**, and **why** an error occurred.

### Simple Definition

> **Error Tracing is the process of identifying failed requests and locating the exact service, operation, or code that caused the error.**

---

# Why Do We Need Error Tracing?

Imagine your application has multiple services.

```text
                User
                  │
                  ▼
             API Gateway
                  │
      ┌───────────┴───────────┐
      ▼                       ▼
 Login Service          Payment Service
      │                       │
      ▼                       ▼
 Oracle Database       Payment Gateway
```

A customer reports:

> "Payment failed."

Without Error Tracing:

* Check application logs
* Check API logs
* Check database logs
* Check payment gateway logs
* Takes a long time to find the issue

With Datadog Error Tracing:

* Open the failed trace
* See the exact service that failed
* View the error message
* View the stack trace
* Find the root cause within minutes

---

# How Error Tracing Works

```text
User Request
      │
      ▼
Application
      │
      ▼
Datadog APM
      │
      ▼
Error Detected
      │
      ▼
Trace Marked as Error
      │
      ▼
Datadog Backend
      │
      ▼
Error Dashboard
```

When an application throws an exception or returns an error status (such as HTTP 500), Datadog marks the trace as an **Error Trace**.

---

# What Information Does Error Tracing Capture?

Datadog captures:

* Error Message
* Exception Type
* Stack Trace
* Failed Service
* Failed Span
* Trace ID
* Span ID
* Timestamp
* Host Name
* Environment
* HTTP Status Code
* Request URL
* Duration
* Service Version

---

# Example

Suppose a user logs in.

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
Database Connection Failed
```

Datadog marks this request as:

```text
Status : ERROR

Reason : Database Connection Timeout

Trace ID : 123456789
```

---

# Example Error Trace

```text
Trace ID : abc123

API Gateway
      │
      ▼
Login Service
      │
      ▼
Authentication
      │
      ▼
Oracle Query
      │
      ✖ ERROR
      │
Database Timeout
```

Here, the **Oracle Query** span is marked as failed.

---

# Error Trace Details

```text
Service         : login-service

Operation       : POST /login

Environment     : Production

Host            : app-server-01

Status          : Error

HTTP Code       : 500

Duration        : 3.5 sec

Exception       : SQLException

Message         : Connection Timeout
```

---

# Stack Trace

Datadog also displays the stack trace.

Example:

```text
java.sql.SQLException: Connection Timeout

at OracleConnection.connect()

at LoginService.login()

at LoginController.login()
```

This helps developers identify the exact location of the error in the code.

---

# Error Types

Common errors monitored by Datadog:

### Application Errors

* NullPointerException
* IndexOutOfBoundsException
* RuntimeException

---

### Database Errors

* Connection Timeout
* Deadlock
* Slow Query
* Authentication Failure

---

### HTTP Errors

* 400 Bad Request
* 401 Unauthorized
* 403 Forbidden
* 404 Not Found
* 500 Internal Server Error
* 503 Service Unavailable

---

### Network Errors

* Connection Refused
* DNS Failure
* Socket Timeout

---

### Cloud Errors

* AWS API Failure
* GCP Authentication Error
* Azure Resource Unavailable

---

# Searching Error Traces

Datadog lets you search only failed traces.

Examples:

Search all errors:

```text
status:error
```

Errors in production:

```text
env:production status:error
```

Errors for a specific service:

```text
service:payment-service status:error
```

Errors with HTTP 500:

```text
http.status_code:500
```

Errors taking longer than 5 seconds:

```text
status:error duration:>5s
```

---

# Root Cause Analysis

Suppose users report that payments are failing.

Datadog Trace:

```text
Payment API
      │
      ▼
Payment Service
      │
      ▼
Payment Gateway
      │
      ✖ ERROR
```

Datadog shows:

```text
HTTP 500

Gateway Timeout

Duration

8 seconds
```

The root cause is immediately visible.

---

# Real Project Example (Your Data Migration Project)

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

Suppose migration fails.

Datadog Trace:

```text
Migration API

      │

      ▼

Striim Processing

      │

      ▼

Cloud Spanner Write

      │

      ✖ ERROR
```

Datadog shows:

```text
Status

ERROR

Reason

Cloud Spanner Write Timeout

Duration

10 Seconds
```

You can immediately identify that the write operation to Cloud Spanner is failing.

---

# Benefits of Error Tracing

* Detect application errors quickly
* Identify failed services
* View stack traces
* Find the exact failed span
* Perform root cause analysis
* Reduce Mean Time to Resolution (MTTR)
* Improve application reliability
* Troubleshoot production issues faster

---

# Error Tracing Workflow

```text
User Request
      │
      ▼
Application
      │
      ▼
Exception Occurs
      │
      ▼
Datadog Agent Captures Trace
      │
      ▼
Datadog Backend
      │
      ▼
Error Trace
      │
      ▼
Dashboard
      │
      ▼
DevOps / Developer
```

---
## Q1. What is Error Tracing in Datadog APM?

**Answer:**

Error Tracing is a feature of Datadog APM that captures failed requests, exceptions, and error-related information. It helps identify the exact service, span, and operation where an error occurred, enabling faster troubleshooting and root cause analysis.

---

## Q2. What information is available in an Error Trace?

**Answer:**

An Error Trace typically includes:

* Trace ID
* Span ID
* Service Name
* Operation Name
* Error Message
* Exception Type
* Stack Trace
* HTTP Status Code
* Duration
* Environment
* Host
* Timestamp
* Service Version

---

## Q3. How does Error Tracing help DevOps engineers?

**Answer:**

Error Tracing helps DevOps engineers quickly identify failed requests, determine which service or operation caused the failure, analyze stack traces, correlate errors with logs and infrastructure metrics, and reduce incident resolution time in production environments.

---

# APM – Profiling (Datadog Continuous Profiler)

## What is Profiling?

**Profiling** is the process of continuously analyzing how your application's code executes while it is running. It helps identify which methods, functions, or lines of code consume the most **CPU**, **memory**, **time**, or other resources.

Unlike APM traces, which show the flow of a request, **Profiling shows what the application is doing inside the code.**

### Simple Definition

> **Profiling helps you identify which parts of your application code are consuming the most resources, so you can optimize performance.**

---

# Why Do We Need Profiling?

Suppose users report:

* Application is slow
* CPU usage is very high
* Memory usage keeps increasing
* Server performance degrades over time

Without profiling:

* Developers manually analyze code
* Guess which function is slow
* Difficult to identify the exact problem

With Datadog Profiling:

* Shows which methods consume the most CPU
* Shows memory allocation
* Identifies inefficient code
* Detects performance bottlenecks

---

# How Profiling Works

```text
                 User Request
                      │
                      ▼
                Java Application
                      │
          Datadog Profiler Enabled
                      │
      Collects CPU, Memory, Threads
                      │
                      ▼
               Datadog Agent
                      │
                      ▼
             Datadog Backend
                      │
      ┌───────────────┼────────────────┐
      ▼               ▼                ▼
 CPU Profile     Memory Profile   Thread Profile
```

---

# What Does Datadog Profiling Monitor?

It continuously collects:

* CPU Usage
* Memory Allocation
* Thread Activity
* Method Execution Time
* Garbage Collection (GC)
* Heap Usage
* Lock Contention
* I/O Wait Time

---

# Example

Suppose your Java application has three methods.

```text
Login()

↓

ValidateUser()

↓

DatabaseQuery()
```

Execution time:

```text
Login()             10 ms

ValidateUser()      20 ms

DatabaseQuery()    950 ms
```

Datadog Profiling immediately shows:

**DatabaseQuery()** is consuming most of the execution time.

---

# CPU Profiling

CPU profiling identifies which methods consume the most processor time.

Example

```text
CPU Usage

DatabaseQuery()     70%

Authentication()    15%

Logging()            5%

Other Methods       10%
```

Result:

DatabaseQuery() is the CPU bottleneck.

---

# Memory Profiling

Memory profiling identifies where memory is allocated.

Example

```text
Memory Allocation

Image Processing     400 MB

Cache                250 MB

Database Objects     150 MB
```

This helps detect excessive memory usage.

---

# Thread Profiling

Shows thread activity.

Example

```text
Running Threads

Main Thread

Worker Thread

Database Thread

GC Thread
```

Useful for detecting blocked or stuck threads.

---

# Heap Profiling

Shows how heap memory is used.

Example

```text
Heap Size

Allocated

1.5 GB

Used

1.3 GB

Free

200 MB
```

Useful for detecting memory leaks.

---

# Garbage Collection (GC)

Datadog monitors Java Garbage Collection.

Example

```text
GC Pause

Normal

20 ms

Today

350 ms
```

Frequent or long GC pauses may slow the application.

---

# Profiling vs Tracing

| APM Tracing                 | Profiling                                  |
| --------------------------- | ------------------------------------------ |
| Shows the path of a request | Shows what happens inside the code         |
| Focuses on request latency  | Focuses on CPU, memory, and code execution |
| Identifies slow services    | Identifies slow methods/functions          |
| Used for request analysis   | Used for code optimization                 |

---

# Profiling Example

Suppose users complain that login is slow.

### APM Trace shows:

```text
Login API

↓

Authentication

↓

Database Query

↓

Response
```

Total response time:

```text
2 Seconds
```

You know the request is slow, but not **why**.

### Profiling shows:

```text
DatabaseQuery()     90%

Authentication()     5%

Logging()            3%

Others               2%
```

Now you know that the **DatabaseQuery()** method is consuming most of the CPU time.

---

# Real Project Example (Your Data Migration Project)

Project:

```text
Oracle Database
       │
       ▼
     Striim
       │
       ▼
Migration Application
       │
       ▼
Cloud Spanner
```

Suppose migration is taking 15 minutes instead of 5 minutes.

### APM Trace

Shows:

```text
Migration API

↓

Striim

↓

Cloud Spanner

↓

15 Minutes
```

### Profiling

Shows:

```text
BatchProcessor()       70%

DataValidation()       20%

Logging()               5%

Others                  5%
```

Now developers know that **BatchProcessor()** needs optimization.

---

# Benefits of Profiling

* Identify CPU-intensive methods
* Detect memory leaks
* Analyze thread usage
* Optimize application performance
* Reduce response time
* Improve resource utilization
* Detect excessive Garbage Collection
* Improve application scalability

---

# Difference Between Monitoring, Tracing, and Profiling

| Feature | Monitoring            | Tracing              | Profiling                                  |
| ------- | --------------------- | -------------------- | ------------------------------------------ |
| Focus   | Infrastructure health | Request flow         | Code execution                             |
| Example | CPU, Memory           | Login API → Database | DatabaseQuery() method                     |
| Finds   | High CPU              | Slow request         | Slow function                              |
| Used By | DevOps                | DevOps & Developers  | Mainly Developers (also useful for DevOps) |

---

# End-to-End Flow

```text
User Request
      │
      ▼
Application
      │
      ▼
Datadog Profiler
      │
      ▼
CPU / Memory / Threads
      │
      ▼
Datadog Agent
      │
      ▼
Datadog Backend
      │
      ▼
Profiling Dashboard
      │
      ▼
Performance Optimization
```

---
## Q1. What is Profiling in Datadog APM?

**Answer:**

Profiling is a feature of Datadog APM that continuously analyzes application code execution. It identifies which methods or functions consume the most CPU, memory, and execution time, helping teams optimize application performance.

---

## Q2. What is the difference between Tracing and Profiling?

| Tracing                                  | Profiling                                      |
| ---------------------------------------- | ---------------------------------------------- |
| Tracks the end-to-end flow of a request  | Analyzes code execution inside the application |
| Identifies slow services and requests    | Identifies CPU- or memory-intensive methods    |
| Helps locate bottlenecks across services | Helps optimize application code                |

---

## Q3. How does Profiling help DevOps engineers?

**Answer:**

Profiling helps DevOps engineers verify whether performance issues are caused by inefficient application code rather than infrastructure problems. It enables faster collaboration with developers by identifying CPU hotspots, excessive memory usage, thread contention, or long garbage collection pauses, reducing the time required to resolve production performance issues.

---

# DevOps Perspective

As a **DevOps Engineer**, profiling is useful after deployments or during production incidents.

For example:

* **Monitoring** tells you CPU usage is **95%**.
* **APM Tracing** tells you the **Migration API** is taking **12 seconds**.
* **Profiling** tells you that the **`BatchProcessor()`** method is consuming **80% of CPU time**.

Together, these features help you determine whether the issue is with the infrastructure, the request flow, or the application code itself, allowing faster troubleshooting and better collaboration with developers.
