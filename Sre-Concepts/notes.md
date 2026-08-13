# Site Reliability Engineering (SRE) — Concepts Guide

## 1. What is SRE?

**Site Reliability Engineering (SRE)** is a discipline that applies software engineering principles to infrastructure and operations problems.

The term was coined by Google, where SRE teams are responsible for the **availability, performance, latency, efficiency, and reliability** of large-scale production systems.

### Key Characteristics

* **Engineering-focused teams** — SRE teams are typically staffed by software engineers who apply coding skills to operational problems.
* **Automation** — SREs write code to automate tasks that would otherwise be performed manually, such as monitoring, deployments, incident response, and capacity planning.
* **Limit on toil** — A common Google SRE guideline is that teams should spend no more than **50% of their time on operational ("toil") work**. The remaining time should be spent on engineering, automation, and reliability improvements.

---

## 2. SRE Principles

### Embracing Risk

Systems are never 100% reliable. Pursuing 100% reliability is often wasteful and sometimes impossible.

SRE embraces an acceptable level of risk defined by **SLOs and error budgets**, rather than attempting to achieve perfect reliability.

### Eliminating Toil

**Toil** is manual, repetitive, automatable, tactical work that provides little or no lasting value.

SRE teams actively identify and eliminate toil through automation.

### Monitoring and Observability

Systems must be monitored to:

* Detect problems
* Understand system health
* Troubleshoot issues
* Support data-driven decisions

Common observability signals include:

* **Metrics**
* **Logs**
* **Traces**

### Automation

Automate tasks that are repeatable and safe to automate, such as:

* Deployments
* Scaling
* Failover
* Remediation
* Infrastructure provisioning

Automation reduces human error and frees engineers to focus on higher-value work.

### Simplicity

Simple systems are easier to:

* Understand
* Operate
* Maintain
* Debug

Complexity is treated as a cost that must be justified.

### Blameless Postmortems

When incidents happen, the focus should be on understanding **what went wrong in the system**, rather than identifying someone to blame.

The goal is to:

* Learn from incidents
* Identify systemic problems
* Improve processes
* Prevent recurrence

### Error Budgets

An **error budget** is a quantified allowance for unreliability.

It is generally calculated as:

```text
Error Budget = 100% − SLO
```

For example:

```text
SLO = 99.9%
Error Budget = 0.1%
```

Error budgets help balance the pace of innovation against reliability risk.

---

## 3. SLI, SLO, and SLA

### SLI — Service Level Indicator

An **SLI** is a quantitative measurement of some aspect of a service's behavior.

It is the actual metric used to measure service performance or reliability.

Examples include:

* Request latency
* Error rate
* Throughput
* Availability

Example formula:

```text
SLI = (Good Events / Total Events) × 100
```

---

### SLO — Service Level Objective

An **SLO** is a target value or range for an SLI. It defines what "good enough" reliability looks like.

Example:

> 99.9% of HTTP requests will be served in under 300ms over a rolling 30-day window.

SLOs are generally **internal goals** and are used to calculate the error budget.

```text
Error Budget = 100% − SLO
```

For example:

```text
SLO = 99.9%
Error Budget = 0.1%
```

A 99.9% availability target allows approximately **43 minutes of downtime per 30-day month**.

---

### SLA — Service Level Agreement

An **SLA** is a contractual agreement with customers that defines expected service levels and the consequences if those levels are not met.

Consequences may include:

* Service credits
* Refunds
* Financial penalties

SLAs are **external-facing** and may be legally or commercially binding.

Typically:

```text
SLA < SLO
```

The internal SLO is often stricter than the customer-facing SLA, providing a safety margin.

### SLI vs SLO vs SLA

| Term    | Meaning                 | Purpose                                         |
| ------- | ----------------------- | ----------------------------------------------- |
| **SLI** | Service Level Indicator | Measures actual service performance             |
| **SLO** | Service Level Objective | Defines the internal reliability target         |
| **SLA** | Service Level Agreement | Defines the contractual commitment to customers |

---

## 4. The Four Golden Signals

The **Four Golden Signals** are four key metrics recommended for monitoring distributed systems.

### 1. Latency

**Latency** is the time it takes to service a request.

It is important to distinguish between:

* Latency of successful requests
* Latency of failed requests

Example:

```text
95th percentile latency = 200ms
```

This means 95% of requests completed in 200ms or less.

### 2. Traffic

**Traffic** measures the demand placed on a system.

Examples:

* HTTP requests per second
* Transactions per second
* Concurrent sessions
* Messages per second

### 3. Errors

**Errors** measure the rate at which requests fail.

Errors can be:

* **Explicit** — HTTP 500 errors
* **Implicit** — HTTP 200 response with incorrect content
* **Policy-based** — Response exceeds an agreed threshold and is considered a failure

### 4. Saturation

**Saturation** measures how "full" a service or resource is.

Examples:

* CPU utilization
* Memory utilization
* Disk I/O
* Connection pool usage
* Queue length

Saturation is often a useful **leading indicator** because increasing saturation can predict problems before they become visible errors.

---

## 5. MTTD and MTTR

### MTTD — Mean Time To Detect

**MTTD** is the average time required to detect that an incident is occurring.

```text
MTTD = Total Detection Time / Number of Incidents
```

MTTD can be improved through:

* Proactive monitoring
* Effective alerting thresholds
* Synthetic checks
* Anomaly detection
* Better observability

---

### MTTR — Mean Time To Resolve / Repair / Recovery

**MTTR** is the average time required to fully resolve or recover from an incident.

Depending on the organization, MTTR may mean **Mean Time to Resolve, Repair, or Recovery**.

```text
MTTR = Total Resolution Time / Number of Incidents
```

---

## Related Reliability Metrics

| Metric   | Meaning                                                                       |
| -------- | ----------------------------------------------------------------------------- |
| **MTTA** | Mean Time To Acknowledge — time from alert to a human acknowledging it        |
| **MTTD** | Mean Time To Detect — time from issue start to detection                      |
| **MTTR** | Mean Time To Resolve/Repair/Recovery — time from detection to full resolution |
| **MTBF** | Mean Time Between Failures — average time between failures or incidents       |

---

## Quick Summary

```text
SLI → What are we measuring?
SLO → What reliability target do we want?
SLA → What do we promise our customers?
Error Budget → How much unreliability can we tolerate?

Four Golden Signals:
1. Latency
2. Traffic
3. Errors
4. Saturation

Incident Metrics:
MTTD → How quickly did we detect the problem?
MTTA → How quickly did someone acknowledge it?
MTTR → How quickly did we resolve/recover from it?
MTBF → How long between failures?
```

