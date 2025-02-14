Here are detailed notes on the OWASP Top 10 (2021) for Web Application Security:

1. Broken Access Control

Improper enforcement of user permissions leads to unauthorized data access, modifications, or actions.

Examples: Viewing or modifying other users’ accounts, bypassing admin controls, accessing APIs without proper authorization.

Prevention: Implement role-based access control (RBAC), enforce least privilege, and perform access control checks on the server side.


2. Cryptographic Failures (Previously "Sensitive Data Exposure")

Weak encryption, missing encryption, or improper storage of sensitive data like passwords, financial info, and personal data.

Examples: Using weak hashing (e.g., MD5), transmitting passwords in plaintext, exposing database backups.

Prevention: Use strong encryption (AES-256, RSA), TLS for data in transit, and proper key management.


3. Injection

Attackers inject malicious data (e.g., SQL, NoSQL, OS commands, LDAP queries) to manipulate or exploit an application.

Examples: SQL injection (' OR '1'='1), command injection (; rm -rf /), XSS (inserting malicious scripts into web pages).

Prevention: Use prepared statements, input validation, and escape user inputs properly.


4. Insecure Design (New in 2021)

Security flaws in the application's architecture and logic, rather than implementation mistakes.

Examples: Lack of threat modeling, weak session management design, not considering security at the design phase.

Prevention: Implement secure design principles, conduct security reviews, and use threat modeling techniques.


5. Security Misconfiguration

Applications and servers running with insecure default settings, unnecessary features, or missing security headers.

Examples: Default admin credentials, unnecessary services running, directory listing enabled, missing security headers (e.g., Content Security Policy).

Prevention: Regular security audits, disable unused features, use automated configuration management tools.


6. Vulnerable and Outdated Components

Using outdated libraries, plugins, or dependencies that have known vulnerabilities.

Examples: Running outdated WordPress plugins, using old versions of jQuery with known security issues, unpatched OS libraries.

Prevention: Regularly update components, use tools like OWASP Dependency-Check, and prefer well-maintained libraries.


7. Identification and Authentication Failures (Previously "Broken Authentication")

Weak authentication mechanisms allow attackers to bypass login protections.

Examples: Weak passwords, no multi-factor authentication (MFA), exposed session IDs, improper password reset mechanisms.

Prevention: Implement MFA, enforce strong password policies, use secure session management techniques.


8. Software and Data Integrity Failures (New in 2021)

Issues related to unverified integrity of software updates, CI/CD pipelines, and insecure deserialization.

Examples: Installing software updates from untrusted sources, tampered update mechanisms, using unsigned code.

Prevention: Verify updates using digital signatures, implement integrity checks in software pipelines.


9. Security Logging and Monitoring Failures

Lack of proper logging and monitoring prevents detection of security breaches and incident response.

Examples: No logging of failed login attempts, missing audit logs, delayed breach detection.

Prevention: Implement centralized logging, use SIEM solutions, set up alerts for suspicious activities.


10. Server-Side Request Forgery (SSRF) (New in 2021)

Attackers trick the server into making requests to unintended locations, potentially accessing internal services.

Examples: An attacker submits a request to fetch data from internal endpoints like http://localhost/admin.

Prevention: Validate and sanitize URLs, enforce allowlists, and disable unnecessary HTTP redirections.

