**Title:** Session Management and Security Policy
**Status:** Accepted
**Date:** 2026-02-03

**Context:**
The auth-service manages both authentication and authorization, but session handling requires standardization. Current approaches to token refresh, session expiry, and revocation are inconsistent, risking security gaps and poor user experience.

**Decision:**

1. **Session Handling:**

   * Maintain **stateless sessions** via JWT access and refresh tokens.
   * Access tokens expire quickly (15 min) to limit risk; refresh tokens expire after 7 days.
   * Tokens include issued-at and expiration claims for validation.

2. **Refresh & Rotation:**

   * Refresh tokens are rotated on each use.
   * Expired or revoked tokens are rejected by middleware.

3. **Revocation Mechanism:**

   * Track active refresh tokens in the database or a fast in-memory store (e.g., Redis).
   * Provide endpoints for users/admins to revoke sessions or logout.

4. **Security Measures:**

   * Enforce HTTPS for all endpoints.
   * Rate-limit authentication and token endpoints to prevent brute-force attacks.
   * Log invalid or suspicious token usage.

5. **Integration:**

   * Middleware validates tokens, checks revocation list, and injects user context into requests.
   * Compatible with RBAC defined in ADR-0201.

**Consequences:**

* Provides clear, secure handling of sessions and token lifecycle.
* Supports user logout and token revocation.
* Aligns with JWT-based authentication strategy while improving operational security.

**References:**

* OWASP Session Management Cheat Sheet
* RFC 7519: JSON Web Token (JWT)
