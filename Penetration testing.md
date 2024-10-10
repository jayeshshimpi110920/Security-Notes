| Vulnerability               | Description                                         | Causes                                       | Mitigation Strategies                        |
|-----------------------------|-----------------------------------------------------|----------------------------------------------|---------------------------------------------|
| SQL Injection               | Allows attackers to execute arbitrary SQL queries. | Unsanitized user input in SQL queries.      | Use prepared statements and parameterized queries. |
| Cross-Site Scripting (XSS) | Injects malicious scripts into web pages.          | Improper validation of user input.           | Validate and sanitize inputs; use CSP.     |
| Command Injection           | Executes arbitrary commands on the host OS.        | Unsanitized inputs passed to system commands.| Validate and sanitize inputs; use APIs.    |
| Remote File Inclusion (RFI) | Allows attackers to include remote files.          | Unsanitized user input for file inclusion.   | Validate file paths; disable dangerous functions. |
| Local File Inclusion (LFI)  | Includes local files that can lead to information disclosure. | Unsanitized file paths in user input.     | Restrict file access and validate inputs.  |
| Insecure Direct Object References (IDOR) | Allows unauthorized access to objects.      | Lack of access control on user inputs.      | Implement proper access controls.          |
| Buffer Overflow             | Overwrites memory by exceeding buffer limits.      | Poor memory management in applications.     | Use safe functions; implement bounds checking. |
| Cross-Site Request Forgery (CSRF) | Tricks users into submitting unwanted requests. | Lack of anti-CSRF tokens in forms.         | Use anti-CSRF tokens; validate requests.   |
| Denial of Service (DoS)    | Overwhelms a service, making it unavailable.       | Resource exhaustion or vulnerabilities.     | Implement rate limiting and traffic filtering. |
| Security Misconfiguration   | Default settings or misconfigurations leading to vulnerabilities. | Human error or default settings left unchanged.| Regularly review and update configurations. |
| Insecure Deserialization    | Manipulation of serialized objects leading to code execution. | Unsanitized data during deserialization.   | Implement integrity checks; avoid deserialization of untrusted data. |
| Broken Authentication       | Flaws allowing attackers to compromise user accounts. | Weak password policies; session management issues. | Use strong authentication mechanisms; enforce session expiration. |
| Sensitive Data Exposure     | Inadequate protection of sensitive data in transit or at rest. | Lack of encryption or weak cryptographic practices. | Use strong encryption; implement data masking. |
| Insufficient Logging and Monitoring | Lack of logging for attacks and breaches.   | Poor logging practices; lack of monitoring. | Implement comprehensive logging; conduct regular audits. |
| Directory Traversal         | Accessing restricted directories or files on the server. | Unsanitized input for file paths.          | Validate file paths; implement proper access controls. |
| Race Conditions             | Exploiting timing issues in concurrent operations. | Poor synchronization in applications.       | Implement proper locking mechanisms.       |
| Unvalidated Redirects and Forwards | Redirecting users to untrusted locations.  | Lack of validation on redirect URLs.       | Validate redirect URLs against a whitelist. |
| Clickjacking                | Trick users into clicking on something different from what they perceive. | Lack of framebusting techniques.           | Use X-Frame-Options header; implement framebusting. |
| Code Injection              | Injecting malicious code into an application.      | Unsanitized input in code execution paths.  | Validate and sanitize inputs; use safe APIs. |
| Credential Stuffing         | Using stolen credentials to gain unauthorized access. | Poor password practices; data breaches.     | Implement multi-factor authentication; rate limit login attempts. |
| Path Traversal             | Accessing unauthorized files by manipulating file paths. | Lack of input validation.                   | Sanitize file paths; use a whitelist for file access. |
| XML External Entity (XXE)   | Exploiting XML parsers to access internal files.   | Poorly configured XML parsers.              | Disable DTD processing; use safe XML libraries. |
| Session Fixation            | Attacker hijacks a valid session ID to gain unauthorized access. | Weak session management practices.          | Regenerate session IDs after authentication. |
