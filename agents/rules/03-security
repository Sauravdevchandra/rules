# AI Secure Development Rules

## Purpose

These rules apply to every AI coding assistant or autonomous coding agent working in this repository.

Security takes priority over convenience, speed, code brevity, and feature completion.

The AI MUST treat all generated code as potentially production-bound unless explicitly told otherwise.

---

# 1. Core Security Principles

The AI MUST:

* Follow secure-by-default design.
* Apply least privilege.
* Use defense in depth.
* Minimize attack surface.
* Fail securely.
* Never trust client-side validation.
* Treat all external input as untrusted.
* Validate authorization server-side.
* Minimize sensitive data collection and exposure.
* Prefer established security libraries over custom security implementations.
* Consider abuse cases, not only normal use cases.
* Preserve existing security controls when modifying code.

The AI MUST NOT weaken security merely to make code work.

If a requested implementation creates a serious vulnerability, explain the risk and implement a safer alternative.

---

# 2. Secrets and Credentials

NEVER hardcode:

* API keys
* passwords
* database credentials
* private keys
* access tokens
* refresh tokens
* JWT secrets
* OAuth client secrets
* service-role keys
* encryption keys
* webhook secrets
* cloud credentials

Use environment variables or an approved secret-management system.

Never expose server secrets through:

* frontend bundles
* browser JavaScript
* public environment variables
* API responses
* logs
* error messages
* source control

Never commit `.env` files containing real credentials.

Provide `.env.example` using placeholders where appropriate.

If credentials appear in source code, warn that they should be removed and rotated.

---

# 3. Authentication

Authentication MUST be performed using established, maintained libraries or trusted identity providers.

Never implement custom password hashing or authentication cryptography.

Passwords MUST:

* never be stored in plaintext
* never be logged
* use established password hashing algorithms through trusted libraries

Prefer modern algorithms such as Argon2id or bcrypt where applicable.

Authentication errors should avoid unnecessary account-existence disclosure.

Sensitive authentication operations should have appropriate rate limiting.

---

# 4. Authorization

Authentication is NOT authorization.

Every protected operation MUST verify authorization server-side.

Never rely on:

* hidden UI elements
* frontend route guards
* JavaScript checks
* disabled buttons
* client-provided roles

for security.

Check ownership, roles, permissions, tenant, and organization boundaries on the server.

Prevent IDOR/BOLA vulnerabilities.

For resources such as:

`/users/{id}`

never assume that an authenticated user may access the supplied ID.

Verify that the requester is authorized to access that specific resource.

Default to deny when permission cannot be determined.

---

# 5. Input Validation

Treat ALL external data as untrusted.

This includes:

* HTTP request bodies
* query parameters
* route parameters
* headers
* cookies
* uploaded files
* webhook payloads
* database-derived untrusted content
* third-party API responses
* message queues
* environment-controlled external input

Validate:

* type
* format
* length
* range
* allowed values
* structure

Prefer allowlists over blocklists.

Perform validation server-side even when frontend validation exists.

---

# 6. SQL and Database Security

NEVER construct SQL using untrusted string concatenation.

Bad:

`SELECT * FROM users WHERE email = '${email}'`

Use:

* parameterized queries
* prepared statements
* safe ORM/query-builder APIs

Prevent:

* SQL injection
* NoSQL injection
* ORM injection
* unsafe dynamic queries

Database accounts should use minimum required privileges.

Never expose administrative database credentials to clients.

---

# 7. Multi-Tenant Security

For multi-tenant applications, every relevant database operation MUST enforce tenant boundaries.

Never trust a client-provided:

* tenant_id
* organization_id
* company_id
* user_id
* account_id

without verifying it against the authenticated identity.

Queries should explicitly enforce ownership or tenant membership.

Prevent cross-tenant data leakage.

---

# 8. XSS Prevention

Never insert untrusted HTML directly into pages.

Avoid unsafe APIs such as:

* `innerHTML`
* `dangerouslySetInnerHTML`
* equivalent raw HTML rendering mechanisms

unless absolutely necessary and properly sanitized.

Escape output according to context.

Sanitize user-generated HTML using trusted libraries.

Consider:

* stored XSS
* reflected XSS
* DOM-based XSS

when handling user-controlled content.

---

# 9. CSRF Protection

State-changing requests using cookie-based authentication MUST consider CSRF protection.

Use appropriate defenses such as:

* SameSite cookies
* CSRF tokens
* Origin validation
* framework-provided CSRF protection

Do not use GET requests for state-changing operations.

---

# 10. Cookie Security

Sensitive cookies should normally use:

* `HttpOnly`
* `Secure`
* appropriate `SameSite`
* restricted `Path`
* appropriate expiration

Authentication tokens should not be unnecessarily exposed to JavaScript.

Never store highly sensitive credentials in browser storage unless the architecture explicitly requires it and risks have been evaluated.

---

# 11. JWT Security

When using JWTs:

* verify signatures
* verify expiration
* validate issuer when applicable
* validate audience when applicable
* restrict accepted algorithms
* never trust unsigned tokens
* never decode a JWT and treat the payload as authenticated without verification

Keep access tokens short-lived where practical.

Refresh tokens require stronger protection.

Never put passwords or unnecessary sensitive information inside JWT payloads.

Do not log JWTs.

---

# 12. Session Security

Sessions MUST:

* use cryptographically secure identifiers
* expire appropriately
* support logout/revocation where required
* rotate when privilege changes or authentication occurs when appropriate

Prevent:

* session fixation
* session replay
* stolen-token reuse where architecture allows mitigation

Sensitive actions may require recent authentication.

---

# 13. API Security

Every API endpoint MUST consider:

* authentication
* authorization
* input validation
* rate limiting
* data exposure
* abuse prevention
* logging
* error handling

Do not return database objects blindly.

Return only fields required by the client.

Never expose sensitive internal fields.

Use appropriate HTTP methods and status codes.

---

# 14. Mass Assignment

Never blindly pass request bodies into database create/update operations.

Bad concept:

`User.update(req.body)`

Explicitly allow expected fields.

Protect fields such as:

* role
* permissions
* isAdmin
* account balance
* verification state
* ownership
* subscription level
* tenant ID

from unauthorized modification.

---

# 15. File Upload Security

File uploads MUST validate:

* size
* extension
* MIME type
* actual file type where necessary
* filename
* destination

Generate server-side filenames when appropriate.

Prevent:

* path traversal
* executable uploads
* malicious SVG/HTML uploads
* overwrite attacks
* excessive file sizes

Do not trust MIME types supplied by clients.

Store uploads outside executable directories where possible.

---

# 16. Path Traversal

Never directly use user-controlled paths for filesystem access.

Prevent values such as:

`../../etc/passwd`

Resolve paths safely and ensure access remains inside approved directories.

---

# 17. Command Injection

Avoid executing shell commands using user-controlled input.

NEVER concatenate untrusted input into shell commands.

Prefer language APIs over shell commands.

If command execution is unavoidable:

* use safe argument arrays
* strictly validate allowed values
* avoid invoking through a shell

---

# 18. SSRF Prevention

Treat user-controlled URLs as dangerous.

For server-side requests:

* restrict allowed protocols
* consider allowlisting destinations
* block internal/private network destinations where appropriate
* prevent access to cloud metadata endpoints
* validate redirects

Be particularly careful with:

* URL preview systems
* image fetchers
* import-from-URL features
* webhook testers
* PDF generators
* proxy endpoints

---

# 19. Cryptography

NEVER design custom cryptographic algorithms.

Use established libraries.

Use cryptographically secure random-number generators for security-sensitive values.

Do not use insecure algorithms for security purposes, including:

* MD5
* SHA-1
* DES
* ECB mode

Use modern authenticated encryption where encryption is required.

Never hardcode encryption keys.

---

# 20. CORS

Do not use:

`Access-Control-Allow-Origin: *`

for authenticated or sensitive APIs unless the architecture genuinely requires public cross-origin access.

Allow only trusted origins.

Never dynamically reflect arbitrary origins without validation.

---

# 21. Rate Limiting and Abuse Protection

Apply rate limiting to sensitive operations such as:

* login
* registration
* password reset
* OTP generation
* OTP verification
* email sending
* SMS sending
* expensive searches
* file uploads
* AI endpoints
* payment operations

Consider both account-based and IP/device-based abuse controls where appropriate.

Do not rely exclusively on frontend cooldown timers.

---

# 22. Error Handling

Do not expose:

* stack traces
* SQL queries
* filesystem paths
* internal service names
* secrets
* credentials
* tokens
* unnecessary infrastructure details

to end users.

Return safe errors externally.

Log useful diagnostic information internally without logging sensitive values.

---

# 23. Logging

Security-relevant events should be logged where appropriate.

Examples:

* authentication failures
* permission failures
* administrative actions
* account changes
* suspicious requests
* security-sensitive configuration changes

NEVER log:

* passwords
* access tokens
* refresh tokens
* session cookies
* private keys
* payment card data
* secret API keys

Redact sensitive values.

---

# 24. Dependencies

Before introducing a dependency:

* verify that it is necessary
* prefer actively maintained packages
* avoid suspicious or abandoned packages
* prefer official packages where available
* avoid packages with known critical vulnerabilities

Do not invent package names.

Never automatically replace secure established libraries with custom implementations.

Keep dependencies pinned or constrained appropriately for the ecosystem.

---

# 25. Supply Chain Security

Do not execute untrusted installation scripts without review.

Be cautious with:

* post-install scripts
* downloaded binaries
* GitHub scripts
* curl-pipe-shell commands
* third-party CI actions

Pin CI/CD actions and dependencies appropriately.

Never expose repository secrets to untrusted pull requests.

---

# 26. Webhooks

Webhook endpoints MUST verify authenticity.

Use:

* cryptographic signatures
* shared secrets
* timestamp validation where supported

Never trust webhook payloads solely because they reach the webhook URL.

Prevent replay attacks when supported.

Return quickly and process expensive work asynchronously where appropriate.

Webhook handlers should be idempotent where duplicate delivery is possible.

---

# 27. OAuth Security

OAuth implementations MUST validate relevant security parameters.

Use:

* `state`
* PKCE where appropriate
* exact redirect URI validation

Never accept arbitrary redirect URLs.

Prevent open redirects.

Tokens must be stored securely.

---

# 28. Password Reset

Password-reset tokens MUST:

* be cryptographically random
* expire
* be single-use where practical
* be stored securely
* not leak through logs

Do not reveal whether an account exists unnecessarily.

Invalidate or rotate relevant sessions after security-sensitive password changes when appropriate.

---

# 29. OTP Security

OTPs MUST:

* expire quickly
* have attempt limits
* be single-use
* be generated securely

Never log OTP values.

Protect OTP-generation endpoints against abuse.

---

# 30. Cloud Security

Never expose cloud administrative credentials to clients.

Apply least privilege to:

* IAM roles
* service accounts
* storage permissions
* serverless functions
* CI/CD credentials

Do not make storage buckets public unless explicitly required.

Security rules and IAM policies should default to deny.

---

# 31. Supabase Security

When Supabase is used:

RLS SHOULD be enabled on tables containing user or sensitive application data.

Policies MUST verify the authenticated user's access.

Never expose:

`SUPABASE_SERVICE_ROLE_KEY`

to frontend code.

The service-role key must only exist in trusted server environments.

Never assume the Supabase anonymous key provides authorization by itself.

Use RLS for database-level protection.

Test policies against unauthorized access and cross-user access.

---

# 32. Firebase Security

Do not rely solely on frontend Firebase checks.

Firestore, Realtime Database, and Storage security rules MUST enforce access.

Never deploy permissive production rules such as unrestricted read/write access.

Validate ownership server-side or through security rules.

---

# 33. Backend Framework Security

For frameworks such as:

* Laravel
* Express
* NestJS
* Django
* Flask
* FastAPI
* Spring
* Rails
* ASP.NET

use built-in security mechanisms where possible.

Do not disable framework security protections simply to bypass errors.

Use official validation, authentication, authorization, ORM, CSRF, and escaping features where applicable.

---

# 34. Frontend Security

Frontend code MUST never contain trusted secrets.

Assume users can:

* inspect JavaScript
* modify requests
* manipulate local storage
* alter cookies accessible to JavaScript
* call APIs directly
* bypass UI restrictions

Therefore frontend authorization checks are UX controls, not security boundaries.

---

# 35. Mobile Security

Do not assume mobile applications can keep embedded secrets confidential.

Avoid embedding privileged API credentials in APK/IPA/application bundles.

Use secure platform storage for sensitive tokens when appropriate.

Validate security-sensitive actions server-side.

---

# 36. AI / LLM Security

Treat AI-generated and AI-consumed content as untrusted.

Never allow LLM output to directly perform privileged operations without appropriate validation and authorization.

Protect against:

* prompt injection
* indirect prompt injection
* tool abuse
* data exfiltration
* insecure output handling
* excessive agency

Do not place secrets unnecessarily inside prompts.

When an AI system can call tools, restrict each tool to minimum necessary permissions.

Validate AI-generated URLs, commands, SQL, HTML, filenames, and code before execution.

---

# 37. Payment Security

Never store raw payment card information unless the system is explicitly designed and certified to do so.

Prefer established payment providers.

Verify payment status server-side.

Never trust payment success information sent by the frontend.

Verify payment-provider webhooks.

Amounts, currencies, products, discounts, and subscription permissions MUST be validated server-side.

---

# 38. Race Conditions

For operations involving:

* payments
* inventory
* credits
* balances
* quotas
* subscriptions
* one-time tokens

consider concurrency and race conditions.

Use:

* database transactions
* atomic operations
* locks
* uniqueness constraints
* idempotency keys

where appropriate.

---

# 39. Sensitive Data

Collect only data required for the feature.

Avoid exposing:

* passwords
* tokens
* government identifiers
* financial information
* private user information
* internal administrative metadata

Mask sensitive information when displayed or logged.

Use encryption in transit.

Use encryption at rest when required by the application's risk profile.

---

# 40. HTTP Security Headers

For web applications, consider appropriate headers such as:

* Content-Security-Policy
* Strict-Transport-Security
* X-Content-Type-Options
* Referrer-Policy
* Permissions-Policy
* frame-ancestors via CSP

Avoid insecure header configurations.

---

# 41. Redirect Security

Never redirect users to arbitrary URLs supplied by request parameters without validation.

Prefer relative application paths or allowlisted domains.

Prevent open redirect vulnerabilities.

---

# 42. Regular Expressions

Avoid regex patterns vulnerable to catastrophic backtracking when processing attacker-controlled input.

Consider input-size limits.

---

# 43. Denial-of-Service Protection

Consider resource exhaustion for:

* uploads
* JSON payloads
* XML
* regex
* image processing
* PDF processing
* database queries
* AI requests
* recursive operations

Set reasonable:

* body limits
* upload limits
* timeouts
* pagination
* concurrency limits

---

# 44. API Responses

Expose only required information.

Never blindly serialize complete:

* user records
* database models
* authentication objects
* payment objects
* internal exceptions

Use explicit response schemas.

---

# 45. Production Configuration

Production MUST NOT use:

* debug mode
* development credentials
* permissive CORS
* public admin endpoints
* default passwords
* verbose error pages
* unrestricted database permissions

Separate development, staging, and production configuration.

---

# 46. Destructive Operations

Before generating commands that:

* delete databases
* drop tables
* remove storage
* destroy infrastructure
* rewrite Git history
* delete production data

the AI MUST clearly identify the destructive effect.

Prefer reversible approaches.

Recommend backups for high-risk migrations or destructive changes.

Never silently introduce destructive operations.

---

# 47. Existing Security Controls

When editing existing code:

DO NOT remove or bypass:

* authentication
* authorization
* validation
* RLS policies
* CSRF protection
* security middleware
* encryption
* rate limiting
* audit logging

unless the replacement provides equivalent or stronger protection.

---

# 48. Security Review Before Completion

Before considering security-sensitive code complete, review for:

1. Authentication
2. Authorization
3. Input validation
4. Injection
5. XSS
6. CSRF
7. SSRF
8. IDOR/BOLA
9. Secrets exposure
10. Sensitive data exposure
11. Rate limiting
12. Error leakage
13. Logging leakage
14. Session/token security
15. Database permissions
16. File upload vulnerabilities
17. Path traversal
18. Command injection
19. Dependency risk
20. Race conditions
21. Tenant isolation
22. Business-logic abuse

---

# 49. Security Finding Severity

When reviewing code, classify meaningful findings as:

CRITICAL
Immediate compromise, authentication bypass, remote code execution, exposed production credentials, major data access, or equivalent impact.

HIGH
Serious authorization bypass, SQL injection, significant sensitive-data exposure, SSRF to sensitive infrastructure, or similar.

MEDIUM
Security weakness requiring realistic conditions or having limited impact.

LOW
Defense-in-depth issue or low-impact security improvement.

INFO
Security hardening recommendation without an identified exploitable vulnerability.

For CRITICAL and HIGH findings, clearly explain:

* vulnerable code
* attack scenario
* impact
* recommended fix

---

# 50. AI Behavior When Writing Code

Before generating security-sensitive code, the AI should reason about trust boundaries.

When implementing a feature:

1. Identify untrusted inputs.
2. Identify authenticated actors.
3. Identify authorization requirements.
4. Identify sensitive data.
5. Identify privileged operations.
6. Identify external systems.
7. Consider abuse cases.
8. Implement appropriate controls.
9. Review the result for vulnerabilities.

Security controls should be included in the initial implementation rather than left as optional future work.

---

# 51. Never Fix Security by Disabling Security

The AI MUST NOT solve errors by recommending actions such as:

* disabling SSL verification
* disabling certificate validation
* disabling authentication
* disabling authorization
* disabling CSRF protection
* disabling RLS
* making databases publicly accessible
* setting unrestricted CORS
* exposing service credentials
* bypassing signature verification

except for clearly isolated testing situations where the risk is explicitly explained and the configuration cannot reach production.

Prefer fixing the root cause.

---

# 52. Security Standards

Use recognized security guidance where relevant, including:

* OWASP Top 10
* OWASP API Security Top 10
* OWASP ASVS
* OWASP Cheat Sheet Series
* CWE
* relevant platform security documentation

For payment systems, consider PCI DSS requirements.

For cloud systems, follow the cloud provider's security best practices.

---

# 53. Final Security Rule

When there is a conflict between:

* convenience
* development speed
* fewer lines of code
* feature behavior

and a meaningful security requirement:

SECURITY WINS.

Never knowingly introduce a serious vulnerability simply because the requested implementation is easier.

When a secure implementation changes expected behavior, explain the tradeoff and provide the secure implementation.
