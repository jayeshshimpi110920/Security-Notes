## OWASP TOP 10
![download](https://github.com/user-attachments/assets/72cbde83-5fed-4a9f-9854-8fde1390152d)

---
The **OWASP Top 10** is a list of the ten most critical security risks to web applications, published by the **Open Web Application Security Project (OWASP)**. It serves as a guide to help developers, testers, and security professionals understand and mitigate the most common security vulnerabilities in web applications. Below is an explanation of each OWASP Top 10 vulnerability, its impact, and key ways to prevent or mitigate it.

---

### **1. Broken Access Control (A01:2021)**

**Description**: 
Broken access control occurs when users can access resources or functionalities they are not authorized to. This can lead to unauthorized information disclosure, modification, or deletion of data.

**Consequences**:
- Unauthorized access to sensitive information.
- Modification or deletion of user accounts or data.
- Escalation of privileges.

**Prevention**:
- Enforce proper access control mechanisms (least privilege principle).
- Use role-based access control (RBAC).
- Ensure sensitive actions require appropriate authorization.
- Regularly test and audit access control rules.

---

### **2. Cryptographic Failures (A02:2021)**

**Description**:
Previously known as "Sensitive Data Exposure," cryptographic failures occur when sensitive data (like passwords or credit card numbers) are not adequately protected in storage or transit.

**Consequences**:
- Exposure of sensitive information (e.g., passwords, PII, financial data).
- Data theft or leakage.
- Compliance violations (e.g., GDPR, PCI DSS).

**Prevention**:
- Use strong encryption algorithms (AES, RSA) for sensitive data.
- Enforce HTTPS for data transmission.
- Store passwords using secure hashing algorithms (bcrypt, PBKDF2).
- Ensure secure key management practices.

---

### **3. Injection (A03:2021)**

**Description**:
Injection flaws occur when untrusted data is sent to an interpreter as part of a command or query. This can lead to the execution of unintended commands (e.g., SQL, NoSQL, LDAP, OS commands).

**Consequences**:
- Data breaches.
- Data loss or corruption.
- Remote code execution.

**Prevention**:
- Use prepared statements or parameterized queries.
- Validate and sanitize user inputs.
- Use ORM (Object Relational Mapping) tools.
- Avoid dynamically constructing queries with user inputs.

---

### **4. Insecure Design (A04:2021)**

**Description**:
Insecure design covers the lack of security controls or the failure to anticipate potential attack vectors during the design and architecture of applications.

**Consequences**:
- Applications may be vulnerable to various attacks due to weak design principles.
- Exploitable flaws in business logic or authentication mechanisms.

**Prevention**:
- Implement secure design principles (e.g., threat modeling, secure design patterns).
- Regularly review and update the application’s architecture.
- Conduct regular security assessments during the design phase.

---

### **5. Security Misconfiguration (A05:2021)**

**Description**:
This vulnerability occurs when security settings are not configured correctly or left at their default values. This includes incorrect permissions, enabling unnecessary features, and misconfiguring web servers or databases.

**Consequences**:
- Exposure of sensitive data.
- Access to unintended resources.
- Exploitation of default configurations or passwords.

**Prevention**:
- Use secure default settings and configurations.
- Disable unnecessary features or services.
- Regularly review and update configurations.
- Implement proper error handling to avoid leakage of sensitive information.

---

### **6. Vulnerable and Outdated Components (A06:2021)**

**Description**:
Using components (libraries, frameworks, plugins) with known vulnerabilities or outdated versions can expose applications to attacks.

**Consequences**:
- Exploitation of known vulnerabilities in components.
- Data breaches, unauthorized access, or system takeover.

**Prevention**:
- Regularly update software dependencies and components.
- Use vulnerability scanning tools to identify outdated components.
- Replace unsupported or end-of-life components.
- Implement a dependency management policy.

---

### **7. Identification and Authentication Failures (A07:2021)**

**Description**:
This category covers weaknesses in user authentication and session management, allowing attackers to compromise passwords, session tokens, or exploit other flaws to assume another user’s identity.

**Consequences**:
- Account takeover.
- Unauthorized access to sensitive data or features.
- Credential stuffing attacks.

**Prevention**:
- Enforce multi-factor authentication (MFA).
- Secure session management (e.g., proper session expiration, secure cookie flags).
- Use strong password policies and secure storage for passwords (hashing).

---

### **8. Software and Data Integrity Failures (A08:2021)**

**Description**:
This vulnerability arises when software updates, critical data, or CI/CD pipelines lack integrity validation. Examples include trusting data from untrusted sources or failing to verify the integrity of third-party software updates.

**Consequences**:
- Code or data manipulation.
- Supply chain attacks (e.g., tampered updates).

**Prevention**:
- Implement digital signatures for code and data integrity verification.
- Use trusted repositories and package management systems.
- Regularly monitor and audit CI/CD pipelines for integrity.

---

### **9. Security Logging and Monitoring Failures (A09:2021)**

**Description**:
This vulnerability occurs when security-critical events are not logged or monitored. Without proper logging and monitoring, attacks may go undetected.

**Consequences**:
- Failure to detect security breaches.
- Delayed incident response.
- Loss of forensic data after an attack.

**Prevention**:
- Enable detailed logging for security-relevant actions (login attempts, data access).
- Implement continuous monitoring and alerting systems.
- Regularly review logs for suspicious activity.
- Use centralized logging solutions to correlate logs from multiple sources.

---

### **10. Server-Side Request Forgery (SSRF) (A10:2021)**

**Description**:
SSRF flaws allow an attacker to make the server perform unauthorized requests to internal or external services. This can expose sensitive internal systems or allow attackers to bypass network protections.

**Consequences**:
- Access to internal resources and services.
- Potential exposure of sensitive data.
- Possible pivoting to further exploit internal systems.

**Prevention**:
- Restrict URLs that the server can request.
- Implement input validation and whitelisting for URLs.
- Block requests to internal IP ranges (e.g., 127.0.0.1, 169.254.x.x).
- Enforce proper authentication for access to internal resources.

---

Here’s a cheat sheet summarizing the **OWASP Top 10 (2021)**:

---

### **OWASP Top 10 Cheat Sheet (2021 Edition)**

| **Risk**                               | **Description** | **Impact** | **Prevention** |
|----------------------------------------|----------------|------------|----------------|
| **1. Broken Access Control (A01)**     | Users can access data or perform actions they are not authorized to. | Unauthorized access, data modification, privilege escalation. | Implement least privilege, use role-based access control (RBAC), and enforce proper authorization checks. |
| **2. Cryptographic Failures (A02)**    | Sensitive data (e.g., passwords, credit cards) is exposed due to weak encryption or insecure handling. | Data theft, compliance violation (GDPR, PCI). | Use strong encryption (e.g., AES), enforce HTTPS, and secure password storage (e.g., bcrypt). |
| **3. Injection (A03)**                 | Untrusted data is sent to interpreters (SQL, NoSQL, OS commands) leading to unintended execution. | Data loss, remote code execution, breaches. | Use prepared statements, parameterized queries, input validation, and avoid dynamic queries. |
| **4. Insecure Design (A04)**           | Security weaknesses in the design phase make the application inherently insecure. | Broad attack surface, logical flaws, business logic vulnerabilities. | Implement threat modeling, secure design patterns, and security reviews during design. |
| **5. Security Misconfiguration (A05)** | Improper configuration of software or hardware settings, using default settings. | Unauthorized access, sensitive information disclosure. | Regular configuration reviews, disable unused features, use secure defaults. |
| **6. Vulnerable and Outdated Components (A06)** | Use of outdated or vulnerable software libraries, frameworks, or plugins. | Exploitation of known vulnerabilities, remote code execution, data breach. | Regularly update components, use tools to check for vulnerable dependencies, and retire end-of-life components. |
| **7. Identification and Authentication Failures (A07)** | Weaknesses in authentication or session management, allowing attackers to assume user identities. | Account takeover, credential stuffing, unauthorized access. | Implement MFA, secure password storage, session timeout, and proper session management. |
| **8. Software and Data Integrity Failures (A08)** | Integrity of software updates, critical data, or CI/CD pipelines is not verified. | Code manipulation, supply chain attacks, malicious updates. | Use digital signatures, ensure proper verification of third-party software, and secure CI/CD pipelines. |
| **9. Security Logging and Monitoring Failures (A09)** | Inadequate logging and monitoring make it difficult to detect and respond to security incidents. | Undetected breaches, slow incident response, loss of forensic data. | Implement centralized logging, enable detailed logs for critical actions, and use real-time monitoring and alerts. |
| **10. Server-Side Request Forgery (SSRF) (A10)** | Server is tricked into making unauthorized requests to internal or external services. | Access to internal resources, sensitive data leakage, network bypass. | Restrict URLs the server can request, use input validation, block internal IP ranges (127.0.0.1, 169.254.x.x). |

---

### **General Tips**:
- **Automate security testing**: Use tools like SAST (Static Application Security Testing) and DAST (Dynamic Application Security Testing) in your CI/CD pipeline.
- **Use security frameworks**: Leverage frameworks that offer built-in security features.
- **Training**: Regularly train developers on secure coding practices and common vulnerabilities.
- **Penetration testing**: Regularly conduct manual and automated penetration testing.

---

This cheat sheet provides a concise reference to understanding the OWASP Top 10 and how to mitigate each vulnerability.

### **General Recommendations to Address OWASP Top 10 Vulnerabilities**:
- **Use security frameworks and libraries**: Leverage well-tested libraries that provide built-in security mechanisms.
- **Secure development practices**: Train developers on secure coding techniques and security best practices.
- **Automated security testing**: Incorporate SAST, DAST, and vulnerability scanning into CI/CD pipelines.
- **Regular security assessments**: Conduct regular penetration testing, code reviews, and security audits.
- **Keep up with security patches**: Regularly update all software components to ensure known vulnerabilities are patched.



### **Conclusion**:
The OWASP Top 10 helps developers and organizations focus on the most critical web application security risks. By understanding and addressing these vulnerabilities, organizations can significantly reduce the risk of security breaches.

