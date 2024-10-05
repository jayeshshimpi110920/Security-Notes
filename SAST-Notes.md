**Table of Contain**:

---
# SAST 

# SAST, DAST, and SCA: Key Differences and Concepts

| **Aspect**                        | **SAST (Static Application Security Testing)**                                      | **DAST (Dynamic Application Security Testing)**                                  | **SCA (Software Composition Analysis)**                                          |
|------------------------------------|-------------------------------------------------------------------------------------|---------------------------------------------------------------------------------|---------------------------------------------------------------------------------|
| **Testing Approach**               | White-box testing (analyzes source code or compiled code)                            | Black-box testing (tests the running application without code access)            | Scans third-party libraries and open-source components used in the application  |
| **Phase of Testing**               | Early in the SDLC (during coding or building)                                        | Late in the SDLC (during testing or post-deployment)                             | Throughout the SDLC (when integrating third-party components)                   |
| **Execution Requirement**          | Does not require the application to be executed                                      | Requires a running instance of the application                                   | Does not require code execution; focuses on third-party components              |
| **Access to Source Code**          | Requires access to the application’s source code, bytecode, or binary code           | No access to source code (interacts with the running application)                | Does not analyze source code; focuses on package dependencies and licenses      |
| **Vulnerability Detection**        | Identifies issues in code structure, such as SQL injection, XSS, buffer overflows    | Identifies runtime issues like authentication problems, server misconfigurations | Detects known vulnerabilities in third-party libraries, outdated versions, and license compliance issues |
| **Primary Focus**                  | Code-level vulnerabilities and logic flaws                                          | Runtime vulnerabilities and security loopholes during execution                 | Vulnerabilities in external libraries, outdated dependencies, license risks     |
| **Examples of Vulnerabilities Found** | - SQL Injection<br> - XSS<br> - Buffer Overflows<br> - Hardcoded secrets            | - Insecure authentication<br> - Server misconfigurations<br> - Session management issues | - Outdated libraries<br> - Vulnerable open-source packages<br> - License violations |
| **Automation & CI/CD Integration** | Easily integrated into CI/CD pipelines for continuous scanning                      | Typically used in QA/testing environments; harder to fully automate              | Easily integrated into CI/CD pipelines for ongoing monitoring of third-party components |
| **False Positives**                | Higher likelihood of false positives, as code is analyzed without execution          | Lower likelihood, but can miss vulnerabilities that depend on static conditions  | False positives are rare; vulnerabilities are based on known CVEs and libraries |
| **False Negatives**                | Potentially misses vulnerabilities that only manifest at runtime                     | May miss vulnerabilities that exist in the code but are not exposed in execution | May not catch zero-day vulnerabilities or issues in custom code                 |
| **Best Suited For**                | Early-stage testing to catch vulnerabilities during development                      | Testing the real-world behavior of the application after deployment              | Managing security risks associated with third-party and open-source components  |
| **Output/Reports**                 | Provides detailed reports pointing to specific lines of code with vulnerabilities    | Offers information on runtime behavior, attack vectors, and exploitable vulnerabilities | Lists vulnerable libraries, licenses, and CVEs (Common Vulnerabilities and Exposures) |
| **Advantages**                     | - Detects security flaws early in the SDLC<br> - Pinpoints exact code locations     | - Tests the application in a real-world scenario<br> - Finds runtime vulnerabilities | - Prevents use of known vulnerable libraries<br> - Helps maintain compliance with license obligations |
| **Limitations**                    | - High false positive rate<br> - No runtime context                                 | - Limited insight into code-level issues<br> - Only tests what's exposed during execution | - Doesn't detect custom code issues<br> - May miss newly emerging vulnerabilities |
| **Tools Examples**                 | - Checkmarx<br> - Veracode<br> - Fortify<br> - SonarQube                             | - OWASP ZAP<br> - Burp Suite<br> - Acunetix                                      | - Snyk<br> - WhiteSource<br> - Black Duck                                        |



---
# How to validate result TP/FP

## 1. SQL Injection (SQLi)

### Steps to Validate:
- **Review the Code:** Inspect the code where the SQL query is constructed. Look for signs of dynamic query construction using user input without proper parameterization.
- **Check for Prepared Statements:** Ensure that the application uses prepared statements (parameterized queries) with bind variables instead of concatenating user input directly into the SQL query.
- **Test User Input Paths:** Manually test the user inputs leading to the SQL query. Use common SQLi payloads (e.g., `' OR 1=1 --`) to check if the input is properly sanitized.
- **Check for Input Validation/Sanitization:** Verify whether input validation or sanitization is implemented before reaching the database layer.

**True Positive Indicators:**
- If the query is dynamically constructed with user input and not parameterized.
- User input can be manipulated to alter the structure of the SQL query.

**False Positive Indicators:**
- The input is being handled using prepared statements or parameterized queries.
- Proper input sanitization is applied before constructing the SQL query.

---

## 2. Cross-Site Scripting (XSS)

### Steps to Validate:
- **Review Output Context:** Look at where and how user-supplied data is being rendered in the HTML, JavaScript, or other output contexts (e.g., URL or event handlers).
- **Check for Output Encoding:** Ensure that any user input rendered on the page is properly encoded for the appropriate context (e.g., HTML escaping for HTML content, JavaScript escaping for JavaScript contexts).
- **Test with Payloads:** Manually test the user input fields with typical XSS payloads (e.g., `<script>alert(1)</script>`) to see if they are executed in the browser.
- **Examine the Input Validation Mechanism:** Check if there’s any input validation in place, but remember that encoding is the most effective XSS mitigation.

**True Positive Indicators:**
- User-supplied input is directly rendered in the output without encoding.
- Malicious scripts can be executed in the browser when inputs are manipulated.

**False Positive Indicators:**
- The user input is properly encoded in the output context (HTML, JavaScript).
- Input sanitization or content security policies (CSP) are applied, neutralizing the potential attack vector.

---

## 3. Command Injection

### Steps to Validate:
- **Review System Command Usage:** Look for places where user input is passed into system commands or shell executions (e.g., `exec()`, `system()`, or similar methods).
- **Check for Input Sanitization:** Validate whether user input is sanitized before being passed to the command execution. Ensure that dangerous characters (e.g., `;`, `&&`, `|`) are filtered.
- **Test Inputs:** Manually test the input fields by injecting command terminators or operators (e.g., `; ls`, `&& whoami`) to see if the command can be altered or extended.

**True Positive Indicators:**
- User input is directly passed to the command execution function without validation or sanitization.
- Malicious input can modify or execute additional commands.

**False Positive Indicators:**
- Proper input sanitization is applied (e.g., using a whitelist of allowed characters).
- Safe functions or libraries are used (e.g., using Python’s `subprocess` module with `args` instead of `shell=True`).

---

## 4. Insecure Deserialization

### Steps to Validate:
- **Review Object Deserialization Logic:** Inspect where untrusted data is deserialized into objects. Focus on whether the deserialized objects are from untrusted sources (e.g., user inputs, external APIs).
- **Check for Safe Deserialization Practices:** Validate that safe deserialization methods are used (e.g., using libraries that enforce types or schema validation). Additionally, ensure that no potentially dangerous objects are deserialized.
- **Test with Malformed Input:** Try deserializing tampered or malicious input to see if it leads to unexpected behavior, including code execution.

**True Positive Indicators:**
- The application allows deserialization of arbitrary data without restrictions, potentially leading to object injection or remote code execution.

**False Positive Indicators:**
- Only trusted data sources are deserialized.
- Serialization libraries with strict schema validation or type restrictions are used.

---

## 5. Sensitive Data Exposure

### Steps to Validate:
- **Review Data Handling:** Inspect how sensitive data (e.g., passwords, credit card numbers, personal data) is being handled in the code. Look for places where it might be logged, exposed in error messages, or transmitted without encryption.
- **Check for Encryption:** Validate whether sensitive data is encrypted at rest and in transit using strong encryption algorithms (e.g., AES-256, TLS 1.2+).
- **Test Response Handling:** Manually test whether sensitive data is inadvertently exposed in responses (e.g., as part of JSON data, URLs, or logs).

**True Positive Indicators:**
- Sensitive data is transmitted over an insecure channel (e.g., HTTP instead of HTTPS).
- Sensitive information is logged or included in error messages.

**False Positive Indicators:**
- Strong encryption is used both in transit (TLS) and at rest.
- No sensitive data is exposed in logs or error responses.

---

## 6. Insecure Direct Object References (IDOR)

### Steps to Validate:
- **Review Access Control Checks:** Inspect areas where user input is used to access resources (e.g., file IDs, user IDs) and ensure proper access control checks are in place.
- **Test with Tampered Inputs:** Manually test by changing input values (e.g., modifying a URL to access another user’s data or object) to see if access control mechanisms prevent unauthorized access.

**True Positive Indicators:**
- A user can modify input values to access or manipulate resources that they do not own or have permission to access.

**False Positive Indicators:**
- Proper access controls are in place (e.g., checks against the logged-in user’s privileges).
- Object references are mapped internally (e.g., via UUIDs or tokens) rather than being directly exposed to the user.

---

## 7. Hardcoded Credentials

### Steps to Validate:
- **Review Code for Credentials:** Search the codebase for hardcoded secrets, such as API keys, database passwords, or tokens.
- **Check Configuration Management:** Verify if credentials are properly managed using environment variables, secure vaults, or configuration files with restricted access.
- **Test Access:** If possible, test whether these credentials can be used to gain unauthorized access to systems.

**True Positive Indicators:**
- Secrets like passwords, API keys, or sensitive tokens are hardcoded in the source code.

**False Positive Indicators:**
- Credentials are not hardcoded, and sensitive information is managed securely (e.g., via a configuration management system or environment variables).

---

## 8. Buffer Overflow

### Steps to Validate:
- **Review Code for Unsafe Functions:** Look for the use of unsafe functions in languages like C/C++ (e.g., `strcpy()`, `sprintf()`, or `gets()`) that do not enforce proper bounds checking.
- **Check for Input Length Validations:** Ensure that proper input length validation and bounds checking are in place before writing to memory buffers.
- **Test with Large Inputs:** Manually test the input fields with excessively large inputs to determine if they trigger crashes or lead to out-of-bounds memory access.

**True Positive Indicators:**
- There is no bounds checking, and user-supplied input can overflow a buffer, potentially leading to crashes or arbitrary code execution.

**False Positive Indicators:**
- The code implements proper bounds checking and uses safe functions (e.g., `snprintf()` or memory-safe libraries).

---

## 9. Cross-Site Request Forgery (CSRF)

### Steps to Validate:
- **Review Form Submissions and API Calls:** Ensure that forms and state-changing operations (e.g., POST requests) include CSRF tokens that are unique per session and request.
- **Test Without CSRF Tokens:** Attempt to replicate state-changing actions without the presence of a valid CSRF token to see if the request is processed.
- **Check Token Validation Logic:** Ensure that the application validates CSRF tokens on the server side before processing requests.

**True Positive Indicators:**
- State-changing operations can be executed without the presence of a CSRF token, or the token is predictable.

**False Positive Indicators:**
- CSRF tokens are present and properly validated on the server side.
