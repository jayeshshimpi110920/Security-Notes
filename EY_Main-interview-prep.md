## SAST (Static Application Security Testing) vs DAST (Dynamic Application Security Testing)

### SAST (Static Application Security Testing)
- **Type:** White-box testing
- **How it works:** Analyzes source code, bytecode, or binaries without executing the application.
- **Goal:** Identify vulnerabilities early in the development lifecycle (before the app is running).
- **Best for:** Detecting issues like SQL injection, cross-site scripting (XSS), and insecure configurations in the code.
- **Pros:**
  - Can be performed early in development.
  - Helps catch vulnerabilities in the codebase.
- **Cons:**
  - May produce false positives.
  - Can be difficult to detect runtime issues like misconfigurations or authentication problems.

### DAST (Dynamic Application Security Testing)
- **Type:** Black-box testing
- **How it works:** Tests the application in its running state (runtime), simulating attacks on the live system.
- **Goal:** Find vulnerabilities that could be exploited in a running application (e.g., during a penetration test).
- **Best for:** Identifying runtime issues like authentication flaws, improper session management, and vulnerabilities exposed through APIs.
- **Pros:**
  - Tests real-world, running applications.
  - Helps identify issues that only appear during execution.
- **Cons:**
  - Requires a live environment or staging server.
  - Can't detect issues in the code that aren't exposed at runtime.

### Key Differences:
- **SAST** focuses on source code, while **DAST** focuses on running applications.
- **SAST** is more effective earlier in development, while **DAST** tests vulnerabilities in live systems.

---

SAST Tools -
1) checkmarx - Not a open source tool
2) SonarQube - Open source static code analysis with some vulnerabilitiy detection.
3) Semgrep - open source -

---



