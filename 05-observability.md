# Observability Reflection

## Signals That Should Have Alerted Earlier

The incident should have been detected earlier through signals related to SMS delivery success, Twilio API behavior, and background job performance.


## Metric 1 – SMS Delivery Success Rate

Measures the percentage of successfully delivered SMS messages relative to total send attempts.

**Why it matters**

This metric directly reflects user impact. A drop indicates that drivers are not receiving critical dispatch notifications.


## Metric 2 – Twilio API Error Rate

Measures the percentage of failed requests to the Twilio API.

**Why it matters**

Helps detect issues with external providers or integration errors such as authentication failures or rate limits.


## Metric 3 – SMS Queue Depth / Processing Latency

Tracks the number of SMS messages waiting in the queue or the time required to process them.

**Why it matters**

Identifies backlog, slow workers, or degraded background job performance.


## Alert

Trigger an alert when SMS delivery success rate drops below 95% for 5 minutes.

**Why**

This focuses on real user impact rather than internal system metrics.


## Dashboard

A dashboard should visualize the full SMS pipeline:

- SMS requests generated
- Queue depth
- SMS send attempts
- Twilio API responses
- SMS delivery success rate

This helps engineers quickly identify where failures occur in the pipeline.