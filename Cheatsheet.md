```
1. Vulnerability Types

Injection Attacks

SQL Injection (SQLi): Manipulating SQL queries via input fields.
Prevention: Use parameterized queries or ORM.

Command Injection: Injecting OS commands via input.
Prevention: Avoid direct OS command execution, sanitize inputs.

Cross-Site Scripting (XSS)
Stored XSS: Malicious script is stored on the server (e.g., in a database).
Reflected XSS: Malicious script reflected in user input (e.g., URL).
Prevention: Use output encoding, Content Security Policy (CSP).


Cross-Site Request Forgery (CSRF)
Explanation: Forces users to execute unwanted actions.
Prevention: Implement CSRF tokens, use SameSite cookie attribute.


Broken Authentication
Issues: Weak password policies, poor session management.
Prevention: Enforce strong password policies, use MFA, secure session tokens.


Insecure Direct Object Reference (IDOR)
Explanation: Attackers manipulate object references to access unauthorized data.
Prevention: Implement proper access control checks.


Insecure Deserialization
Explanation: Attackers exploit insecure deserialization mechanisms to execute code remotely.
Prevention: Avoid serialization of sensitive objects, validate input.


Broken Access Control
Explanation: Unauthorized access to resources.
Prevention: Use proper authorization mechanisms and test for access control issues.


2. Common Attack Techniques
Brute Force Attack
Explanation: Guessing credentials through trial and error.
Prevention: Limit login attempts, use CAPTCHA.

Session Hijacking
Explanation: Stealing valid session cookies to impersonate a user.
Prevention: Use Secure, HttpOnly flags on cookies, ensure SSL/TLS.

Privilege Escalation
Explanation: Exploiting vulnerabilities to gain higher access levels.
Prevention: Apply the principle of least privilege, keep systems patched.

Man-in-the-Middle (MITM)
Explanation: Attacker intercepts communication between two parties.
Prevention: Use strong encryption (SSL/TLS), secure communication channels.


3. OWASP Top 10 (2021)

1. Broken Access Control
2. Cryptographic Failures
3. Injection
4. Insecure Design
5. Security Misconfiguration
6. Vulnerable and Outdated Components
7. Identification and Authentication Failures
8. Software and Data Integrity Failures
9. Security Logging and Monitoring Failures
10. Server-Side Request Forgery (SSRF)


4. Security Headers

X-Frame-Options: Prevents clickjacking (DENY or SAMEORIGIN).
X-Content-Type-Options: Prevents MIME type sniffing (nosniff).
Strict-Transport-Security (HSTS): Enforces HTTPS for a domain.
Content-Security-Policy (CSP): Controls resources that can be loaded on a page.

5. Tools for Penetration Testing

Burp Suite
Used For: Intercepting requests, scanning for vulnerabilities, fuzzing.
Key Features: Proxy, Repeater, Intruder, Scanner.


OWASP ZAP
Used For: Automated scanning and manual testing of web applications.
Key Features: Passive and active scans, fuzzing, session management.


Nmap
Used For: Network discovery and vulnerability scanning.
Key Features: Port scanning, OS detection, service version detection.


SQLMap
Used For: Automated detection and exploitation of SQL injection vulnerabilities.


Nessus
Used For: Vulnerability scanning of networks, applications, and systems.


6. Steps for Penetration Testing

1. Reconnaissance (Information Gathering):
Tools: Nmap, Recon-ng, Whois, theHarvester.
Gather data about the target (IP addresses, DNS, open ports).

2. Scanning:
Tools: Nmap, OWASP ZAP.
Identify open ports, services, and vulnerabilities.

3. Exploitation:
Tools: Metasploit, Burp Suite, SQLMap.
Exploit discovered vulnerabilities (SQLi, XSS, etc.).

4. Post-Exploitation:
Tools: Mimikatz, Meterpreter.
Escalate privileges, maintain access, pivot to other systems.

5. Reporting:
Document vulnerabilities, exploitation steps, and recommendations for remediation.

7. Vulnerability Assessment vs. Penetration Testing
Vulnerability Assessment: Identifies and prioritizes security vulnerabilities but does not exploit them.
Penetration Testing: Simulates an actual attack to exploit vulnerabilities and evaluate security controls.

8. Common Preventive Measures
Input Validation: Sanitize user inputs to prevent SQLi, XSS, and other injection attacks.
Access Control: Implement least privilege and role-based access controls.
Logging and Monitoring: Ensure security events are logged and monitored in real-time.
Encryption: Encrypt sensitive data in transit (TLS) and at rest (AES).

9. Security Testing Types
SAST (Static Application Security Testing): Analyzes code or binaries for vulnerabilities without executing the program.
DAST (Dynamic Application Security Testing): Tests the running application for security vulnerabilities from the outside.
IAST (Interactive Application Security Testing): Combines elements of SAST and DAST by monitoring applications during execution.


