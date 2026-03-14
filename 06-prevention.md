# Prevention & Improvements

## Priority 1 – Introduce a Dedicated SMS Queue with Retry Policy and Dead Letter Queue (DLQ)

Move SMS delivery into a dedicated asynchronous queue with controlled retry logic, exponential backoff, and a Dead Letter Queue for messages that continue failing after the maximum number of retries.

**Why this matters**

This improves resilience at the infrastructure level. Temporary failures such as provider timeouts or rate limits can be retried safely, while persistent failures are isolated in the DLQ instead of continuously degrading the main SMS processing flow.

A DLQ also gives operational visibility into failed messages, affected accounts, and recurring error patterns. It can be monitored to trigger alerts or follow-up actions when failed SMS volume exceeds a threshold.

**Trade-offs**

- Increased infrastructure and operational complexity
- Requires clear retry policies and duplicate-handling strategy
- DLQ helps contain failures, but does not replace fixing the root cause


## Priority 2 – Strengthen Monitoring and Release Validation for SMS Changes

Introduce stronger release controls and monitoring around SMS-related changes, including automated validation in CI/CD, post-deployment checks, and alerting based on SMS delivery health and DLQ growth.

This should include:
- validation of required environment variables and SMS configuration
- tests for SMS job logic and payload generation
- monitoring of SMS success rate, retry volume, and DLQ size
- a runbook defining what to do when failed SMS messages accumulate

**Why this matters**

The incident followed a production change to the SMS cron job. Stronger deployment validation and operational monitoring reduce the probability of regressions reaching production and improve detection speed when failures occur.

**Trade-offs**

- More effort is required to maintain tests, alerts, and operational procedures
- CI/CD pipelines may become slower
- Teams need discipline to keep runbooks and monitoring aligned with system changes