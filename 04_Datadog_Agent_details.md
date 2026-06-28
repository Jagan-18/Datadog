# What is a Software Integration?

Software integration is the process of combining to separate isolated software pieces to work together.

---

# How Datadog Agent works?

The Datadog Agent is software that runs on your hosts. After installation it automatically starts to collects events and metrics from hosts and sends them to Datadog, where you can search, filter, aggregate and alert on information. The Datadog Agent acts like a middle layer between your application and Datadog website.

The main components are two:

1. **Collector** – which collects data from your host on every 15 seconds

2. **Forwarder** – which sends data to Datadog over https

The main configuration file is:

`C:\ProgramData\Datadog\datadog.yaml`

Configuration files for Integrations are in:

`C:\ProgramData\Datadog\conf.d`

---

## Diagram Flow

```text
                    Datadog Agent

+--------------------+         HTTP
|     Collector      | ----------------------\
+--------------------+                        \
                                               \
                                                > TCP:17123
                                               /
+--------------------+         HTTP           /
| DogStatsD          | ----------------------/
|   (optional)       |
+--------------------+

                           |
                           v

                  +------------------+
                  |    Forwarder     |
                  +------------------+
                           |
                           | HTTPS/443
                           |
                     +-------------+
                     |  Firewall   |
                     +-------------+
                           |
                           v

                  +------------------+
                  |   Datadog SaaS   |
                  +------------------+
```


