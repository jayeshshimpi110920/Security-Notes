### **Common Vulnerabilities and Exposures (CVE) - Quick Notes**  

#### **1. What is CVE?**  
CVE stands for **Common Vulnerabilities and Exposures**. It is a **publicly available database** of known security vulnerabilities in software and hardware. Each vulnerability is assigned a unique **CVE ID** for easy tracking and reference.  

#### **2. Structure of a CVE ID**  
A CVE ID follows this format:  
**CVE-YYYY-NNNNN**  
- **CVE** → Prefix indicating it's a vulnerability.  
- **YYYY** → Year of disclosure.  
- **NNNNN** → Unique identifier for that vulnerability.  
  - Example: **CVE-2021-44228** (Log4j vulnerability).  

#### **3. Where CVE Data Comes From**  
- Reported by security researchers, vendors, and organizations.  
- Maintained by **MITRE Corporation** in partnership with the **National Vulnerability Database (NVD)**.  

#### **4. How CVEs Are Rated?**  
CVEs are rated using **CVSS (Common Vulnerability Scoring System)**, which assigns a severity score from **0 to 10**:  
- **Low (0.1 - 3.9)** → Minimal impact.  
- **Medium (4.0 - 6.9)** → Moderate risk.  
- **High (7.0 - 8.9)** → Significant risk.  
- **Critical (9.0 - 10.0)** → Requires immediate action.  

#### **5. How to Find CVE Details?**  
- **NVD Database:** [https://nvd.nist.gov/vuln/search](https://nvd.nist.gov/vuln/search)  
- **MITRE CVE List:** [https://cve.mitre.org/](https://cve.mitre.org/)  

#### **6. Handling CVEs in Software**  
- **Identify vulnerable dependencies** using SCA tools (e.g., Snyk, OWASP Dependency-Check).  
- **Analyze severity** and impact on your application.  
- **Apply patches or update** to a fixed version.  
- **Monitor for new CVEs** in CI/CD pipelines.  

#### **7. Real-World Examples of CVEs**  
1. **CVE-2021-44228** - Log4j Remote Code Execution (RCE).  
2. **CVE-2017-5638** - Equifax data breach (Apache Struts vulnerability).  
3. **CVE-2014-0160** - Heartbleed bug (OpenSSL security flaw).  
