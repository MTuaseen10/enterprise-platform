Title: Event-Driven Notification Architecture
Status: Accepted
Date: 2026-02-03

Context:
The notification-service must deliver real-time notifications to users across multiple channels (email, SMS, push). Current polling-based approaches are inefficient and cannot scale with increasing events from multiple microservices.

Decision:

Event-Driven Architecture:

Use message broker (e.g., RabbitMQ, Kafka) to publish and consume events.

Each microservice publishes events; notification-service subscribes to relevant topics.

Notification Channels:

Email via transactional email service (e.g., SendGrid).

SMS via provider API (e.g., Twilio).

Push notifications via device tokens and platform SDKs.

Processing & Reliability:

Events are processed asynchronously.

Implement retries with exponential backoff for failed deliveries.

Dead-letter queue for messages that fail after multiple retries.

Scalability & Monitoring:

Horizontal scaling of consumers for high throughput.

Logging, monitoring, and alerting on failed or delayed notifications.

Consequences:

Reduces tight coupling between microservices.

Supports high volume of notifications with low latency.

Ensures reliable delivery with retry and dead-letter mechanisms.

References:

Event-Driven Architecture patterns

Kafka/RabbitMQ best practices
