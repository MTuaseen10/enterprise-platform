Title: User Profile and Preferences Management
Status: Accepted
Date: 2026-02-03

Context:
The user-service handles core user identity and authentication. However, profile information (name, contact, preferences, settings) requires a separate strategy to ensure flexibility, privacy, and maintainability. Mixing identity and profile data risks tightly coupled services and data exposure.

Decision:

Profile Domain Separation:

User identity (authentication, roles, security info) remains in the core user-service.

Profile data (display name, contact info, preferences, settings) stored in a dedicated profile-service or separate database schema.

Data Access & API:

Profile-service exposes APIs for read/write of user profiles.

All updates validated and logged for audit purposes.

Integrates with user-service via service-to-service API calls to enforce identity verification.

Privacy & Security:

Sensitive profile fields encrypted at rest.

Only authorized services and users can access profile data.

GDPR/CCPA compliance enforced for data handling and deletion requests.

Extensibility:

Supports adding new preferences, feature toggles, or profile fields without impacting authentication logic.

Enables downstream services (notifications, recommendations, analytics) to consume profile info via controlled APIs.

Consistency & Events:

Profile changes emit events (ProfileUpdated, PreferencesChanged) for interested services.

Event-driven updates ensure eventual consistency without tight coupling.

Consequences:

Decouples identity/authentication from user profile management.

Provides a flexible and secure way to manage user preferences and settings.

Enables scalable integration with downstream services while maintaining privacy and auditability.

References:

Microservices domain-driven design

GDPR/CCPA data handling standards

Event-driven architecture best practices
