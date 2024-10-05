# Security Concepts and Definitions

1. **What is a security threat?**  
   **Definition:** A security threat is a potential danger that exploits vulnerabilities to harm systems, data, or networks.  
   **Example:** A hacker attempting to gain unauthorized access to a web application.

2. **What is a vulnerability?**  
   **Definition:** A vulnerability is a weakness or flaw in a system, software, or network that can be exploited by threats.  
   **Example:** SQL injection, unpatched software, weak passwords.

3. **What is a security risk?**  
   **Definition:** A security risk refers to the potential damage or loss that could happen when a vulnerability is exploited by a threat.  
   **Example:** Loss of customer data due to a vulnerability being exploited in a web application.

4. **What is the difference between a vulnerability and a threat?**  
   **Definition:** Vulnerability is a weakness in the system, while a threat is something that could exploit that weakness.  
   **Example:** The vulnerability could be an outdated software version, and the threat could be a hacker using an exploit to take control of the application.

5. **What is the OWASP Top 10?**  
   **Definition:** OWASP (Open Web Application Security Project) Top 10 is a list of the most critical security risks to web applications, published by OWASP.  
   **Key Risks:** Injection (e.g., SQL Injection), Broken Authentication, Sensitive Data Exposure, Cross-Site Scripting (XSS), etc.

6. **What is an attack vector?**  
   **Definition:** An attack vector is the path or method used by a hacker to access a system or network and exploit vulnerabilities.  
   **Example:** Phishing emails, malicious URLs, or unpatched software.

7. **What are false positives and false negatives in security testing?**  
   - **False Positive:** When a security tool flags something as a vulnerability, but it is not an actual risk.  
   - **False Negative:** When a security tool misses a real vulnerability that should have been flagged.

8. **What is the principle of least privilege (PoLP)?**  
   **Definition:** This principle states that users or systems should be granted the minimal level of access necessary to perform their job functions to reduce the attack surface.  
   **Example:** An intern should not have admin access to the company’s critical systems.

9. **What is the CIA Triad?**  
   - **Confidentiality:** Ensuring that data is only accessible to those authorized to view it.  
   - **Integrity:** Ensuring that data is accurate and not tampered with.  
   - **Availability:** Ensuring that data and systems are available when needed by authorized users.

10. **What is encryption?**  
    **Definition:** Encryption is the process of converting information into a secure format (ciphertext) that cannot be easily understood by unauthorized people.  
    **Example:** HTTPS encrypts the communication between a browser and a website.

11. **What is a DDoS (Distributed Denial of Service) attack?**  
    **Definition:** A DDoS attack is when multiple systems flood a targeted system (e.g., a server) with traffic, causing it to slow down or become unavailable to legitimate users.  
    **Mitigation:** Using firewalls, load balancers, and intrusion detection systems (IDS).

12. **What is multi-factor authentication (MFA)?**  
    **Definition:** MFA is a security mechanism that requires two or more forms of verification before allowing access.  
    **Example:** A user enters a password and then a code sent to their mobile phone.

13. **What is cross-site scripting (XSS)?**  
    **Definition:** XSS is a vulnerability that allows attackers to inject malicious scripts into web pages viewed by other users.  
    **Mitigation:** Validating and sanitizing user input, using Content Security Policy (CSP).

14. **What is SQL Injection (SQLi)?**  
    **Definition:** SQLi is an attack where an attacker can execute malicious SQL queries against a database by manipulating the user input.  
    **Mitigation:** Using prepared statements and parameterized queries.
