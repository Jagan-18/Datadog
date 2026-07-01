# Datadog – SLA, SLO, SLI, and Error Budget

These four concepts are very important in **Site Reliability Engineering (SRE)** and are widely used in **Datadog** to measure and improve service reliability.

---

# Overview

```text
                Service Reliability

                     │
                     ▼

              SLI (Measurement)

                     │
                     ▼

          SLO (Target / Goal)

                     │
                     ▼

          SLA (Customer Agreement)

                     │
                     ▼

          Error Budget (Allowed Failure)
```

<img width="666" height="212" alt="Image" src="https://github.com/user-attachments/assets/154452a9-b881-4c1d-b266-6d433429fbe5" />

---

# 1. SLI (Service Level Indicator)

## What is SLI?

An **SLI** is a **measurement** that tells you how well your service is performing.

It is a **numeric value** collected from metrics such as:

* Availability
* Response Time
* Error Rate
* Latency
* Throughput

### Simple Definition

> **SLI is the actual measured value of your service performance.**

---

## Examples of SLIs

* API Availability
* Request Success Rate
* API Response Time
* Database Latency
* Error Rate
* Request Throughput

---

## Example

Suppose your Login API handled:

```text
Total Requests = 1000

Successful Requests = 995

Failed Requests = 5
```

SLI:

```text
Availability

995 / 1000

=

99.5%
```

Here,

**SLI = 99.5%**

---

## Another Example

```text
Payment API

Average Response Time

250 ms
```

This is also an SLI.

<img width="1267" height="727" alt="Image" src="https://github.com/user-attachments/assets/c42bbcfc-ff3f-4bfd-a1cb-eaef1d94573d" />

---

# 2. SLO (Service Level Objective)

## What is SLO?

An **SLO** is the **target or goal** that your team wants to achieve.

It is based on one or more SLIs.

### Simple Definition

> **SLO is the target value you want your service to meet.**

---

## Example

Company Target:

```text
API Availability

99.9%
```

This means:

"We want our application to be available at least **99.9%** of the time."

That target is the **SLO**.

---

## More Examples

| Metric              | SLO      |
| ------------------- | -------- |
| Availability        | 99.9%    |
| Login Response Time | < 300 ms |
| Error Rate          | < 1%     |
| Database Latency    | < 100 ms |

<img width="1269" height="733" alt="Image" src="https://github.com/user-attachments/assets/a435e94c-1413-4c50-bbb0-905c87785ffc" />

---

# 3. SLA (Service Level Agreement)

## What is SLA?

An **SLA** is a **formal agreement** between a service provider and a customer.

It defines:

* Expected service quality
* Availability commitment
* Response time commitment
* Penalties if targets are not met

### Simple Definition

> **SLA is a business contract with the customer.**

---

## Example

Company promises:

```text
Service Availability

99.9%

per month
```

If availability falls below 99.9%:

* Customer receives compensation
* Company pays a penalty

This commitment is the SLA.

---

## SLA Example

```text
Customer Contract

Availability

99.95%

Support Response

30 Minutes

Penalty

Yes
```

<img width="1282" height="748" alt="Image" src="https://github.com/user-attachments/assets/9d0a0f6d-1ab4-435d-a256-78cf3180fdb0" />


---
# 4. Error Budget

## What is an Error Budget?

An **Error Budget** is the **maximum amount of failure or downtime that is allowed while still meeting the SLO**.

### Simple Definition

> **Error Budget is the amount of unreliability you can "spend" without violating your SLO.**

---

## Example

SLO:

```text
99.9% Availability
```

Allowed downtime:

```text
100%

-

99.9%

=

0.1%
```

That **0.1%** is the Error Budget.

---

## Monthly Example

30 days:

```text
30 Days

=

43,200 Minutes
```

Error Budget:

```text
0.1%

of

43,200

=

43.2 Minutes
```

Meaning:

Your application may be unavailable for **43.2 minutes** during the month and still meet the 99.9% SLO.

<img width="1074" height="594" alt="Image" src="https://github.com/user-attachments/assets/109b6fd6-bd12-4483-a3f0-fe1a39c66048" />


---

# Relationship Between SLI, SLO, SLA, and Error Budget

```text
               SLI
     (Measured Performance)
               │
               ▼
               99.92%
               │
               ▼
              Compare
               │
               ▼
      SLO = 99.90%
               │
      ┌────────┴─────────┐
      ▼                  ▼
 SLI ≥ SLO          SLI < SLO
      │                  │
      ▼                  ▼
 Healthy Service   SLO Violation
                          │
                          ▼
                Error Budget Consumed
                          │
                          ▼
              Possible SLA Violation
```

---

# Datadog SLO Dashboard

Datadog provides dashboards showing:

```text
Availability

99.92%

Target

99.90%

Remaining Error Budget

72%

Status

Healthy
```

---

# Datadog SLO Example

Suppose:

```text
API Requests

1,000,000
```

Successful:

```text
999,200
```

Failed:

```text
800
```

SLI:

```text
999200

/

1000000

=

99.92%
```

SLO:

```text
99.90%
```

Result:

```text
SLI

99.92%

>

99.90%

SLO Achieved
```

---

# Error Budget Example

Target:

```text
SLO

99.9%
```

Allowed Failure:

```text
0.1%
```

Actual Availability:

```text
99.85%
```

Remaining Budget:

```text
Negative

Budget Exhausted
```

Now the team should focus on improving reliability instead of releasing new features.

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

Possible SLIs:

* Migration Success Rate
* Migration API Response Time
* Pipeline Availability
* Cloud Spanner Write Latency

Example:

```text
Migration Jobs

1000

Successful

998

Failed

2
```

SLI:

```text
99.8%
```

SLO:

```text
99.5%
```

Result:

```text
99.8%

>

99.5%

Target Achieved
```

---

# Difference Between SLA, SLO, SLI, and Error Budget

| Term             | Meaning                                     | Example                  |
| ---------------- | ------------------------------------------- | ------------------------ |
| **SLI**          | Actual measured performance                 | Availability = 99.92%    |
| **SLO**          | Internal target or objective                | Availability ≥ 99.90%    |
| **SLA**          | Contractual commitment to the customer      | 99.90% uptime guaranteed |
| **Error Budget** | Allowed failure while still meeting the SLO | 0.10% downtime allowed   |

---

# Easy Way to Remember

```text
SLI

↓

Measures Reality

↓

SLO

↓

Defines Goal

↓

SLA

↓

Promises Customer

↓

Error Budget

↓

Allowed Failure
```

---

# Interview Questions

## Q1. What is an SLI?

**Answer:**

An SLI (Service Level Indicator) is a quantitative measurement of a service's performance, such as availability, latency, error rate, or throughput. It reflects the actual performance of the service.

---

## Q2. What is an SLO?

**Answer:**

An SLO (Service Level Objective) is the target value for an SLI. It defines the desired level of service reliability or performance, such as maintaining 99.9% availability.

---

## Q3. What is an SLA?

**Answer:**

An SLA (Service Level Agreement) is a formal agreement between a service provider and a customer that defines expected service levels, responsibilities, and potential penalties if the agreed targets are not met.

---

## Q4. What is an Error Budget?

**Answer:**

An Error Budget is the amount of failure or downtime that is acceptable while still meeting the SLO. It helps teams balance innovation and reliability by defining how much unreliability can be tolerated.

---
