# Investigation Plan

## Step 1 – Review Application Logs

I would begin by reviewing Laravel application logs to determine whether SMS sending attempts are occurring and whether any errors are being logged.

**Why**

This quickly confirms whether the system is reaching the SMS sending layer or failing earlier in the workflow.

**What I expect to learn**

- Whether SMS send attempts are triggered
- Whether Twilio-related errors appear
- Whether failures are consistent or account-specific


## Step 2 – Inspect Twilio Console Logs

Next, I would review Twilio delivery logs and API responses.

**Why**

Twilio is a critical external dependency for SMS delivery.

**What I expect to learn**

- Whether Twilio is rejecting requests
- Whether messages are successfully accepted but not delivered
- Whether rate limits or authentication errors are occurring


## Step 3 – Analyze System Metrics

Review infrastructure and job metrics:

- CPU
- memory
- request rate
- cron duration
- queue depth

**Why**

Metrics help detect degraded background workers, queue backlog, or resource constraints.

**What I expect to learn**

- Whether queue depth is increasing
- Whether cron duration is abnormal
- Whether system resources are constrained


## Step 4 – Review CI/CD Pipeline History

Check the deployment history to identify recent changes.

**Why**

Production incidents are frequently caused by recent deployments.

**What I expect to learn**

- Whether SMS-related components were modified
- Whether configuration changes were introduced


## Step 5 – Analyze Account-Specific Patterns

Investigate whether the issue correlates with specific account types.

**Why**

Customer support reports indicate VIP accounts are most affected.

**What I expect to learn**

- Whether failures correlate with specific tenants or configurations
- Whether routing or template differences exist