### **Software Composition Analysis (SCA) - Quick Notes**  

#### **1. What is SCA?**  
SCA is a security practice that identifies and analyzes open-source and third-party components in software to detect **vulnerabilities, license issues, and outdated dependencies**.  

#### **2. Importance of SCA**  
- Prevents security risks from open-source libraries.  
- Ensures **license compliance** (GPL, MIT, Apache, etc.).  
- Helps maintain a **Software Bill of Materials (SBOM)** for transparency.  

#### **3. Vulnerability Management**  
- **CVE (Common Vulnerabilities and Exposures):** Publicly disclosed security flaws.  
- **CWE (Common Weakness Enumeration):** Categorizes software weaknesses.  
- **NVD (National Vulnerability Database):** Centralized vulnerability database.  
- **CVSS (Common Vulnerability Scoring System):** Rates vulnerability severity (0-10).  

#### **4. Open Source Risks & Management**  
- **Security risks:** Exploitable vulnerabilities (e.g., Log4j).  
- **Legal risks:** License violations can lead to lawsuits.  
- **Operational risks:** Outdated dependencies can break applications.  

#### **5. SCA Tools & Techniques**  
Popular SCA tools include:  
- **Snyk**  
- **Black Duck**  
- **WhiteSource (Mend SCA)**  
- **OWASP Dependency-Check**  

**Techniques used:**  
- Scanning package managers (Maven, NPM, Pip, etc.).  
- Comparing dependencies against vulnerability databases.  
- Automating scans in **CI/CD pipelines**.  

#### **6. Remediation & Best Practices**  
- **Prioritize high-risk CVEs** (based on CVSS score).  
- **Patch or upgrade dependencies** regularly.  
- **Use secure dependency management** (lock files, SemVer).  
- **Integrate SCA with DevSecOps** for continuous monitoring.  

#### **7. Real-world Scenarios**  
- **Log4j vulnerability (CVE-2021-44228):** Critical zero-day affecting Java applications.  
- **Heartbleed (OpenSSL bug):** Exposed sensitive data.  
- **Equifax breach:** Caused by an unpatched open-source library (Apache Struts).  
