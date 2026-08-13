Site Reliability Engineering (SRE) — Concepts Guide

1. What is SRE?

Site Reliability Engineering (SRE) is a discipline that applies software engineering principles to infrastructure and operations problems. The term was coined by Google, where SRE teams are responsible for the availability, performance, latency, efficiency, and reliability of large-scale production systems.

Key characteristics:

-SRE teams are typically staffed by software engineers who apply coding skills to operational problems.
-SREs write code to automate tasks that would otherwise be done manually (monitoring, deployments, incident response, capacity planning).
-A guiding rule of thumb: SRE teams should spend no more than 50% of their time on operational ("toil") work; the rest should go to engineering/automation.

2. SRE Principles

-Embracing Risk — Systems are never 100% reliable; pursuing 100% is wasteful and often impossible. SRE embraces an acceptable level of risk defined by SLOs and error budgets rather than chasing perfection.

-Eliminating Toil — Toil is manual, repetitive, automatable, tactical work with no lasting value. SRE actively works to identify and eliminate toil through automation.

-Monitoring and Observability — Systems must be monitored to detect problems, understand system health, and support data-driven decisions (metrics, logs, traces).

-Automation — Automate everything that is repeatable and safe to automate — deployments, scaling, failover, remediation — to reduce human error and free up engineering time.

-Simplicity — Simple systems are easier to understand, operate, and debug. Complexity is treated as a cost that must be justified.

-Blameless Postmortems — When incidents happen, the focus is on understanding what went wrong systemically — not who to blame — to drive genuine learning and prevent recurrence.

-Error Budgets — A quantified allowance for unreliability (100% − SLO), used to balance the pace of innovation against reliability risk.

3. SLI, SLO, SLA
-SLI — Service Level Indicator

A quantitative measure of some aspect of the service's behavior. It's the raw metric.

Examples: request latency (e.g., 95th percentile response time), error rate, throughput, availability.

Formula example: SLI = (Good Events / Total Events) × 100

-SLO — Service Level Objective

A target value or range for an SLI, agreed upon internally, that defines what "good enough" reliability looks like.

Example: "99.9% of HTTP requests will be served in under 300ms over a rolling 30-day window."

SLOs are internal goals — they drive the error budget.
Error Budget = 100% − SLO (e.g., 99.9% SLO → 0.1% error budget, ~43 minutes of downtime/month)

-SLA — Service Level Agreement

A contractual agreement with customers that includes SLOs (usually looser than internal targets) and defines consequences (penalties, credits, refunds) if not met.

SLAs are external-facing, legally/commercially binding.
SLOs are usually set stricter than SLAs to provide a buffer/safety margin

4. The Four Golden Signals
-Latency — The time it takes to service a request. Distinguish latency of successful requests from failed requests.

-Traffic — A measure of demand on the system (HTTP requests/sec, transactions/sec, concurrent sessions).

-Errors — The rate of requests that fail, explicitly (500s), implicitly (200 with wrong content), or by policy (response time over threshold counted as failure).

-Saturation — How "full" the service is — CPU, memory, disk I/O, connection pool usage. Often the best leading indicator, since saturation predicts problems before they cause visible errors.

5. MTTD and MTTR
MTTD — Mean Time To Detect

The average time to discover that an incident is occurring, from the moment it actually started.

MTTD = Total Detection Time (across incidents) / Number of Incidents

Improved through: proactive monitoring, good alerting thresholds, synthetic checks, anomaly detection.

MTTR — Mean Time To Resolve / Repair / Recovery

The average time to fully resolve an incident, from detection (or start) to resolution.

MTTR = Total Resolution Time (across incidents) / Number of Incidents

Related metrics:

Metric	Meaning
MTTA	Mean Time To Acknowledge — time from alert to a human acknowledging it
MTTD	Mean Time To Detect — time from issue start to detection
MTTR	Mean Time To Resolve/Repair — time from detection to full fix
MTBF	Mean Time Between Failures — average time between incidents (reliability measure)

