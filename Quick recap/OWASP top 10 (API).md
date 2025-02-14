OWASP API Security Top 10 (2023) – Explained with Examples

**1. Broken Object Level Authorization (BOLA)**

**Issue**: API doesn’t verify if a user is authorized to access a specific object.

**Example:**

API request: GET /api/user/123/orders

Attacker changes 123 to 124 and accesses another user's order.


**Fix**: Implement proper object-level authorization checks.



**2. Broken Authentication**

**Issue:** Weak authentication allows attackers to impersonate users.

**Example:**

API allows logging in with weak tokens (12345-token).

Attacker guesses or reuses a leaked token to log in.


**Fix:** Enforce strong authentication (OAuth, JWT, MFA).



**3. Broken Object Property Level Authorization**

**Issue:** Users can modify restricted fields in API requests.

**Example:**

PATCH /api/user/123 with {"role": "admin"}

If API lacks property-level validation, a normal user can become an admin.


**Fix:** Restrict access to sensitive fields at the API level.



**4. Unrestricted Resource Consumption**

**Issue:** API allows unlimited requests, leading to excessive resource use.

**Example:**

Attacker sends thousands of requests to GET /api/search?q=item, crashing the system.


**Fix:** Implement rate limiting, quotas, and request validation.



**5. Broken Function Level Authorization**

**Issue:** Regular users access admin-only API functions.

**Example:**

POST /api/admin/delete_user/123

A normal user can delete accounts due to missing authorization checks.


**Fix:** Implement role-based access control (RBAC).



**6. Unrestricted Access to Sensitive Business Flows**

**Issue:** API doesn’t limit automated interactions with sensitive features.

**Example:**

A bot automates unlimited coupon generation (POST /api/coupons/generate).


**Fix:** Add rate limits, CAPTCHAs, and abuse detection mechanisms.



**7. Server-Side Request Forgery (SSRF)**

**Issue:** API fetches URLs without validation, allowing internal network access.

**Example:**

Attacker submits GET /api/fetch?url=http://localhost/admin to access internal data.


**Fix:** Validate and allowlist external URLs.



**8. Security Misconfiguration**

**Issue:** API exposes sensitive data due to misconfigured settings.

**Example:**

Debug mode is enabled, exposing API keys in error messages.


**Fix:** Disable debug mode in production, review configurations.



9. Improper Inventory Management

**Issue:** Exposed old or undocumented APIs create security risks.

**Example:**

GET /api/v1/user-info (old version) is still accessible with weak security.


**Fix:** Maintain an updated API inventory and deprecate old endpoints.



**10. Unsafe Consumption of APIs**



**Issue:** Trusting third-party APIs without security checks.

**Example:**

Application blindly trusts responses from GET /api/external-data, which could be compromised.


**Fix:** Validate and sanitize data from third-party APIs.

