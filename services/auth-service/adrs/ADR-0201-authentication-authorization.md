**Title:** Authentication and Authorization Strategy
**Status:** Accepted
**Date:** 2026-02-03
**Context:**
The auth-service is responsible for securing all APIs and user interactions. We require a standardized, maintainable approach for authenticating users and authorizing access to resources. Current systems are fragmented, with inconsistent token handling and no centralized policy enforcement.
**Decision:**
1. **Authentication**:
   * Use **JWT (JSON Web Tokens)** for stateless authentication.
   * Tokens issued on successful login, signed with a strong secret key stored securely in environment variables.
   * Access tokens have a short TTL (e.g., 15 minutes), refresh tokens longer (e.g., 7 days).
2. **Authorization**:
   * Implement **role-based access control (RBAC)**. Each user has assigned roles, and each role maps to allowed actions on specific resources.
   * Middleware in Express validates JWT and checks user roles before granting access.
3. **Password Management**:
   * Passwords are hashed using **bcrypt** before storage.
   * Enforce strong password policy and optional 2FA for sensitive roles.
4. **Token Revocation & Rotation**:
   * Maintain a blacklist or token versioning to revoke compromised tokens.
   * Refresh tokens can be rotated to limit the impact of token leaks.
5. **Security Considerations**:
   * All endpoints are served over **HTTPS** only.
   * Rate limiting applied to login and token refresh endpoints to mitigate brute-force attacks.
   * Logging and monitoring of failed authentication attempts.
**Consequences:**
* Centralized JWT auth simplifies service-to-service communication.
* RBAC allows fine-grained access control without duplicating logic.
* Token expiration and rotation improve overall security posture.
* Middleware enforces consistent authentication and authorization checks across all APIs.
**References:**
* RFC 7519: JSON Web Token (JWT)
* OWASP Authentication Cheat Sheet

If you want, I can also generate a **shorter, one-page ADR version** that’s minimal but still covers JWT + RBAC. Do you want me to do that?
