Title: User Domain Separation
Status: Accepted
Date: 2026-02-03

Context:
The user-service manages all user-related data and operations across the platform. Currently, user data, authentication, and profile management are mixed with domain-specific logic from other services (orders, subscriptions, notifications). This coupling creates maintenance challenges, security risks, and inconsistent access patterns. Clear separation of the user domain is required to improve modularity, security, and service scalability.

Decision:

Domain Boundaries:

The user-service owns all user data: profiles, roles, preferences, and authentication metadata.

Other services must interact via API endpoints or event-driven messages, never directly accessing user storage.

Role and Access Management:

Define user roles and permissions in a centralized RBAC system.

Roles are enforced across services via JWT claims or service-to-service validation.

Integration:

Expose REST/gRPC endpoints for CRUD operations on user profiles.

Publish user-related events (UserCreated, UserUpdated, UserDeleted) for downstream services.

Security:

Sensitive data (passwords, MFA tokens) is stored securely with encryption and hashing.

Only the user-service handles authentication and authorization decisions.

Scalability:

Stateless API endpoints support horizontal scaling.

Event-driven notifications ensure eventual consistency for downstream services.

Consequences:

Centralizes user management, reducing duplication and inconsistencies.

Improves security and compliance by isolating sensitive data.

Enables easier scaling and maintainability of user-related operations.

References:

Domain-Driven Design (DDD) principles

RBAC and secure user management patterns
