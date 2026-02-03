Title: Order Lifecycle Management
Status: Accepted
Date: 2026-02-03

Context:
The order-service handles creation, processing, and fulfillment of customer orders. Currently, order states are inconsistent across services, and there is no unified approach for lifecycle transitions, making tracking and recovery difficult.

Decision:

Order States:

Define clear lifecycle states: Pending, Confirmed, Processing, Shipped, Delivered, Cancelled, Returned.

Each state transition is validated to ensure business rules (e.g., cannot ship a cancelled order).

Event-Driven Updates:

Publish events for every state change (OrderConfirmed, OrderShipped, etc.) to allow other services (notifications, inventory, billing) to react asynchronously.

Persistence & Audit:

Store orders in a central database with timestamped state history.

Maintain an audit log for all transitions for traceability and dispute resolution.

Error Handling & Recovery:

Failed transitions are retried via a queue.

Manual intervention endpoints for stuck or invalid orders.

Integration:

APIs expose current order status and history.

Compatible with inventory-service and payment-service events.

Consequences:

Provides consistent, auditable lifecycle for all orders.

Facilitates real-time integration with downstream services.

Reduces risk of invalid state transitions and lost orders.

References:

Event-Driven Architecture patterns

Order management best practices
