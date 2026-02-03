Title: Batched Notification Processing
Status: Accepted
Date: 2026-02-03

Context:
For bulk events (e.g., daily reports, summary alerts), sending individual notifications per event can overwhelm channels and users. We need an efficient batching mechanism to group notifications and optimize delivery.

Decision:

Batching Strategy:

Aggregate notifications per user or group over a configurable time window (e.g., 5–15 minutes).

Send combined notifications via a single email/SMS/push message.

Queue & Scheduling:

Events are queued in a message broker.

Scheduled worker collects events, batches them, and triggers delivery.

Failure Handling:

Retry failed batch deliveries.

Maintain logs of failed notifications for auditing.

Monitoring & Metrics:

Track batch sizes, delivery latency, and failure rates.

Alerts if delivery falls below SLA thresholds.

Consequences:

Reduces redundant notifications and provider costs.

Improves user experience by consolidating multiple notifications.

Can coexist with event-driven real-time notifications for urgent events.

References:

Event batching patterns

Notification service best practices
