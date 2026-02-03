Title: Subscription Order Management
Status: Accepted
Date: 2026-02-03

Context:
A related service handles subscription-based orders with recurring billing and deliveries. Traditional order lifecycle is insufficient because subscriptions introduce recurring events, renewals, and cancellations.

Decision:

Subscription States:

Active, Pending Renewal, Paused, Cancelled, Expired.

Recurring billing triggers state transitions automatically.

Event-Driven Workflow:

Publish events for renewal, pause, and cancellation.

Downstream services (billing, notifications, fulfillment) consume events for processing.

Scheduling & Automation:

Use cron or task scheduler to trigger recurring actions.

Automated retries for failed payments or delivery issues.

Persistence & History:

Maintain full subscription history and renewal attempts.

Enable rollback or reactivation of subscriptions if necessary.

Error Handling & Monitoring:

Retry failed payments with exponential backoff.

Track metrics: renewal success rate, failed deliveries, churn.

Consequences:

Supports recurring revenue models with minimal manual intervention.

Keeps subscription state consistent across systems.

Enables seamless integration with billing and fulfillment services.

References:

Recurring billing and subscription management best practices

Event-driven state management
