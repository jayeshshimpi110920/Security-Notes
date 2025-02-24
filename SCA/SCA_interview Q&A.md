1️⃣ **What is Software Composition Analysis (SCA)?**  
   - **SCA is a security practice that scans open-source components for vulnerabilities, license issues, and outdated dependencies.**  

2️⃣ **Why is SCA important?**  
   - **It helps prevent security breaches, ensures compliance, and maintains software integrity.**  

3️⃣ **How is SCA different from SAST and DAST?**  
   - **SCA analyzes dependencies, SAST scans source code, and DAST tests running applications.**  

4️⃣ **What is a CVE?**  
   - **Common Vulnerabilities and Exposures (CVE) is a unique ID assigned to a publicly known security flaw.**  

5️⃣ **Where can you check for CVEs?**  
   - **NVD (nvd.nist.gov) and MITRE CVE database (cve.mitre.org).**  

6️⃣ **What is a CWE?**  
   - **Common Weakness Enumeration (CWE) categorizes software weaknesses that can lead to vulnerabilities.**  

7️⃣ **What is a CVSS score?**  
   - **Common Vulnerability Scoring System (CVSS) rates vulnerability severity (0-10).**  

8️⃣ **What are the main risks of using open-source components?**  
   - **Security vulnerabilities, legal issues, outdated dependencies, and lack of support.**  

9️⃣ **What is a Software Bill of Materials (SBOM)?**  
   - **A list of all components in a software, including libraries and dependencies.**  

🔟 **What are some popular SCA tools?**  
   - **Snyk, Black Duck, WhiteSource (Mend), OWASP Dependency-Check, JFrog Xray.**  

1️⃣1️⃣ **How does an SCA tool detect vulnerabilities?**  
   - **By comparing software dependencies against vulnerability databases (NVD, GitHub Security Advisories, etc.).**  

1️⃣2️⃣ **How does SCA help in DevSecOps?**  
   - **By integrating into CI/CD pipelines to detect vulnerabilities early.**  

1️⃣3️⃣ **How does an SCA tool check for license compliance?**  
   - **It scans dependencies and flags non-compliant licenses (GPL, MIT, Apache, etc.).**  

1️⃣4️⃣ **What is the difference between a direct and a transitive dependency?**  
   - **Direct dependencies are explicitly used, while transitive dependencies come from third-party libraries.**  

1️⃣5️⃣ **How does CVSS scoring impact vulnerability prioritization?**  
   - **Higher CVSS scores (7-10) indicate critical vulnerabilities needing immediate action.**  

1️⃣6️⃣ **What are some common licensing issues in open-source software?**  
   - **GPL enforcement, missing attribution, license incompatibility.**  

1️⃣7️⃣ **How can organizations manage open-source security risks?**  
   - **Use SCA tools, monitor CVEs, update dependencies, follow secure coding practices.**  

1️⃣8️⃣ **What is the impact of outdated dependencies on software security?**  
   - **They may contain unresolved vulnerabilities that can be exploited.**  

1️⃣9️⃣ **What is Semantic Versioning (SemVer)?**  
   - **A versioning system (Major.Minor.Patch) used to track software updates.**  

2️⃣0️⃣ **What is OWASP Dependency-Check, and how does it work?**  
   - **A tool that scans dependencies for known CVEs using the NVD database.**  

---

## **🔹 Hard Level Questions**  

2️⃣1️⃣ **What is the difference between WhiteSource (Mend) and Black Duck?**  
   - **Both are SCA tools, but they differ in integration capabilities, reporting, and compliance tracking.**  

2️⃣2️⃣ **How does SCA help in supply chain security?**  
   - **It prevents software supply chain attacks by identifying vulnerable dependencies.**  

2️⃣3️⃣ **How can organizations automate SCA in CI/CD pipelines?**  
   - **Integrate SCA tools like Snyk or OWASP Dependency-Check into build pipelines.**  

2️⃣4️⃣ **What is the role of SCA in software compliance (e.g., GDPR, PCI-DSS)?**  
   - **Ensures open-source components comply with security and legal standards.**  

2️⃣5️⃣ **What are some challenges in implementing SCA?**  
   - **False positives, scanning large codebases, managing transitive dependencies.**  

2️⃣6️⃣ **How does SCA help mitigate Log4j vulnerabilities?**  
   - **Identifies outdated Log4j versions and recommends updates.**  

2️⃣7️⃣ **How does SBOM help in vulnerability management?**  
   - **Provides visibility into all software components, making it easier to track vulnerabilities.**  

2️⃣8️⃣ **What is the difference between an exploit and a vulnerability?**  
   - **A vulnerability is a weakness; an exploit is an attack that takes advantage of it.**  

2️⃣9️⃣ **What is the risk of not updating dependencies in an application?**  
   - **Potential exposure to known CVEs that attackers can exploit.**  

3️⃣0️⃣ **What is the difference between an open-source license and a proprietary license?**  
   - **Open-source licenses allow modification and distribution, while proprietary licenses restrict usage.**  

---

## **🔹 Scenario-Based & Advanced Questions**  

3️⃣1️⃣ **Your SCA scan detects a high-risk CVE in a library your app depends on, but no patch is available. What do you do?**  
   - **Apply temporary mitigations, remove or replace the library, monitor for a patch.**  

3️⃣2️⃣ **How can SCA help prevent supply chain attacks like SolarWinds?**  
   - **By identifying and tracking all third-party components used in software.**  

3️⃣3️⃣ **Explain how Log4Shell (CVE-2021-44228) was exploited.**  
   - **Attackers executed remote code via JNDI lookups in Log4j logging.**  

3️⃣4️⃣ **How do you handle false positives in SCA reports?**  
   - **Verify manually, cross-check multiple sources, adjust scanning rules.**  

3️⃣5️⃣ **You find an outdated open-source library with no CVE. Should you update it? Why?**  
   - **Yes, to ensure stability, performance, and security improvements.**  

3️⃣6️⃣ **How do you ensure open-source components comply with security policies?**  
   - **Use SBOM, enforce version control, automate scanning, conduct audits.**  

3️⃣7️⃣ **How do you prioritize which vulnerabilities to fix first?**  
   - **Based on CVSS score, exploitability, business impact, and environment.**  

3️⃣8️⃣ **How can an SCA tool differentiate between a vulnerable and a patched version?**  
   - **By analyzing dependency versions against known CVEs.**  

3️⃣9️⃣ **What is the role of NIST in vulnerability management?**  
   - **Maintains the National Vulnerability Database (NVD) for tracking CVEs.**  

4️⃣0️⃣ **How do you prevent dependency confusion attacks?**  
   - **Use private package repositories, pin dependency versions, validate sources.**  

