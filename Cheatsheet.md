OWASP Top 10(open web application security project) -[reduce the risk of security incident by working with world largest community of trusted ethical hackers]
1)Broken Access Control (A01) | Users can access data or perform actions they are not authorized to.|| Unauthorized access, data modification, privilege escalation.||| Implement least privilege, use role-based access control (RBAC), and enforce proper authorization checks.
2)Cryptographic Failures (A02)| Sensitive data (e.g., passwords, credit cards) is exposed due to weak encryption or insecure handling.|| Data theft, compliance violation (GDPR, PCI).||| Use strong encryption (e.g., AES), enforce HTTPS, and secure password storage (e.g., bcrypt).
3)Injection (A03) [ Untrusted data is sent to interpreters (SQL, NoSQL, OS commands) leading to unintended execution.] Data loss, remote code execution, breaches.{ Use prepared statements, parameterized queries, input validation, and avoid dynamic queries.} 
4)Insecure Design (A04) [Security weaknesses in the design phase make the application inherently insecure.] Broad attack surface, logical flaws, business logic vulnerabilities. {Implement threat modeling, secure design patterns, and security reviews during design.}
5)Security Misconfiguration (A05) [ Improper configuration of software or hardware settings, using default settings.]	Unauthorized access, sensitive information disclosure.{Regular configuration reviews, disable unused features, use secure defaults.}
6)Vulnerable and Outdated Components (A06) [ Use of outdated or vulnerable software libraries, frameworks, or plugins.]	Exploitation of known vulnerabilities, remote code execution, data breach.{{ Regularly update components, use tools to check for vulnerable dependencies, and retire end-of-life components.}}
7)Identification and Authentication Failures (A07)[Weaknesses in authentication or session management, allowing attackers to assume user identities.] Account takeover, credential stuffing, unauthorized access. {{{Implement MFA, secure password storage, session timeout, and proper session management.}}}
8)Software and Data Integrity Failures (A08)[ Integrity of software updates, critical data, or CI/CD pipelines is not verified.]  Code manipulation, supply chain attacks, malicious updates. {{ Use digital signatures, ensure proper verification of third-party software, and secure CI/CD pipelines.}}
9)Security Logging and Monitoring Failures (A09) [Inadequate logging and monitoring make it difficult to detect and respond to security incidents.]Undetected breaches, slow incident response, loss of forensic data. {{Implement centralized logging, enable detailed logs for critical actions, and use real-time monitoring and alerts.}}
10)Server-Side Request Forgery (SSRF) (A10)[Server is tricked into making unauthorized requests to internal or external services.]	Access to internal resources, sensitive data leakage, network bypass. { Restrict URLs the server can request, use input validation, block internal IP ranges (127.0.0.1, 169.254.x.x).} 
-------------------------------------------------------------------------------------------------------------------------------------------------------
1)XSS - {{Output encoding, Use CSP(content security policy), input sanitization}}
2)CSRF - Attacker trick a logged-in user into submitting an unwanted request- {{Use anti-CSRF token, same-site cookies and ensure proper user authentication}
3)Insecure deserialization - {it happen when malicious data deserialized without validation}[[remote code execution/data tampering/privilege escalation]] 
4)CORS(cross-origin resource sharing)- its a security features implemented by web brosers that allow or restrict resporces requested from domain outside. It helps to prevent malicious site from accessing sensitive information from another domain.
5)RCE(Remote code execution)-allow attacker to run malicious code on remote system. if exploited, the attacker can take control of the target sys/app, execute arbitrary command -[arise due to various flaw{input validation/inscure deserialization/command injection/buffer overflows} ###sandboxing-run code in isolated environment to limit the impact of RCE if its occurs. @Disable unnecessary features-(plugins/fileupload/command injection) @Firewalls
6)IDOR(insecure direct object reference)=it occures when application exposes internal object(e.g. database records,files or URLs) to users without authorization checks.*can access data belongs to other users ##(data breaches/account takeover/unauthorized actions) @implment roles based access contorl @input sanitization
7)sensitive data exposure - ##Lack of encryption or weak cyptographic pratices@use strong encryption; implement data masking

Security Headers:------------------------------------------------------------------------------------------------------------------------------------
Content-Security-Policy     Prevent XSS, data injection	        Content-Security-Policy: default-src 'self'    [default policy for loading/contorl javascript]
X-Frame-Options	            Prevent Clickjacking                X-Frame-Options: DENY/SAMEORIGIN
X-Content-Type-Options	    Prevent MIME-type sniffing	        X-Content-Type-Options: nosniff
Strict-Transport-Security   Enforce HTTPS	                Strict-Transport-Security: max-age=31536000
X-XSS-Protection	    Basic XSS protection (deprecated)	X-XSS-Protection: 1; mode=block
Referrer-Policy	            Control referrer information	Referrer-Policy: no-referrer
Cross-origin-resource-shareing     Control CORS                	Access-Control-Allow-Origin: https://trusted.com
Set-Cookie (with flags)	    Secure cookie handling		Set-Cookie: Secure; HttpOnly; SameSite=Strict


CVE-Common Vulnerabilities and exposures - 

Broken Authentication - Weak password policy/credential stuffing/session managment issues/lack of MFA/brute force attack/username enumeration/default credentials
Authorization(broken access control) - forced browsing/IDOR/unrestricted file upload/ vertical & horizaontal privilage escalation/bypass access control -{ensure Role-based Access control, user role clearly defined}

HTTP (80), HTTPS (443), FTP (21), SSH (22), and DNS (53).

pre-engagement phase  - 1)understand about scope 2) testing approch 3) legal and compliance
Recon - Passive Recon(WHOIS:gather domain info/identify subdomain/public footprint:social media,data leaks/google dorking)
	Active Recon(port scanning/fingerprinting:identify OS, software and versions /wappalyzer to identify framework and CMS)
Vulnerability identification (network vulnerability scanning/web application vulnerability/APi)


--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
1) Input Validation
	SQL Injection: Try payloads like admin'--, ' OR 1=1--, etc.
	Command Injection: Inject special characters (&, |, ;, $(), etc.) to see if commands are executed.
	LDAP Injection: Inject * or & into fields to test for LDAP queries.
2) Authentication Mechanism
	Weak Password Policy: Test weak passwords (e.g., password123, admin123) and verify password strength requirements.
	Account Lockout: Attempt multiple failed logins (e.g., more than 5 attempts) to see if account lockout or CAPTCHA triggers.
	Brute Force: Use Hydra or Burp Suite Intruder to perform brute force attacks. Check for rate-limiting or CAPTCHA.
	Multi-Factor Authentication (MFA): Check if MFA is enabled and attempt to bypass it (e.g., using token reuse).
3) Session Management
	Session ID in URL: Ensure session IDs are not in the URL (use Burp Suite to check).
	Session Expiration: Confirm session expiration after inactivity and on logout.
	Session Fixation: Test if the session ID changes after login.
4) Error Handling
	Verbose Errors: Check for detailed error messages (e.g., “Invalid Username” vs. “Invalid Password”).
	Username Enumeration: Test if error messages or response times reveal valid usernames.
5. Password Storage
	Hashed Passwords: Confirm passwords are hashed (bcrypt, Argon2) and salted.
	Secure Transmission: Verify password transmission over HTTPS using Burp Suite.
6. CSRF (Cross-Site Request Forgery)
	CSRF Token: Ensure the login form includes a CSRF token. Check if tokens are validated (e.g., using Burp Suite to modify requests).
7. Security Headers
	X-Frame-Options: Set to DENY or SAMEORIGIN to prevent clickjacking.
	Content-Security-Policy (CSP): Ensure CSP is in place to mitigate XSS.
8. Authentication Bypass
	Default Credentials: Try known default credentials (e.g., admin:admin).
	Bypass Techniques: Test parameter tampering and input encoding techniques.
9. CAPTCHA Mechanism
	CAPTCHA Protection: Ensure CAPTCHA works after multiple failed attempts. Test for CAPTCHA bypass using automation.
10. "Remember Me" / Persistent Login
	Cookie Storage: Ensure persistent login tokens are securely stored (HttpOnly, Secure flags).
	Token Expiration: Check if tokens have reasonable expiration and are invalidated after logout.
11. Password Recovery Mechanism
	Token-based Reset: Ensure password reset tokens are long, random, and expire quickly.
	Brute Force Protection: Test for brute-force attacks on recovery questions or tokens.
12. HTTPS and Security
	HTTPS: Ensure the login page and form submission use HTTPS.
	Secure Cookies: Verify session cookies are marked as HttpOnly and Secure.
13. OAuth/OpenID (If Applicable)
	Open Redirects: Test for open redirect issues in OAuth flows.
	Token Handling: Verify proper handling and expiration of OAuth tokens.
14. API Authentication (If Applicable)
	Token-Based Auth: Test for weak or missing token expiration and signature validation.
	API Endpoint Testing: Ensure API endpoints require authentication and are not vulnerable to IDOR.
15. 2FA/MFA (If Applicable)
	Bypass MFA: Attempt to bypass 2FA using session replay or token manipulation.








