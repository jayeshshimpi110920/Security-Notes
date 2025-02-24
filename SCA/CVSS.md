### **Common Vulnerability Scoring System (CVSS) - Quick Notes**  

#### **1. What is CVSS?**  
CVSS (**Common Vulnerability Scoring System**) is a standardized framework for **assessing the severity of security vulnerabilities**. It assigns a **numerical score (0-10)** to a vulnerability, helping security teams prioritize remediation.  

#### **2. CVSS Score Ranges**  
| **Score**  | **Severity Level**  | **Meaning**  |
|------------|--------------------|-------------|
| **0.0**    | None               | No security impact |
| **0.1 - 3.9** | Low              | Minimal risk, may not need immediate action |
| **4.0 - 6.9** | Medium           | Some risk, should be addressed |
| **7.0 - 8.9** | High             | Significant risk, requires attention |
| **9.0 - 10.0** | Critical        | Severe impact, must be fixed immediately |

#### **3. Components of CVSS Score**  
CVSS is divided into three metric groups:  

1️⃣ **Base Score (Mandatory)** – Measures the **intrinsic** characteristics of the vulnerability.  
   - **Attack Vector (AV):** How the attack is executed (Network, Adjacent, Local, Physical).  
   - **Attack Complexity (AC):** How easy the attack is (Low, High).  
   - **Privileges Required (PR):** Level of access required (None, Low, High).  
   - **User Interaction (UI):** Requires user action? (None, Required).  
   - **Impact (CIA Triad - Confidentiality, Integrity, Availability).**  

2️⃣ **Temporal Score (Optional)** – Measures factors that change over time.  
   - Exploitability (Is it actively exploited?).  
   - Remediation Level (Is there a fix available?).  

3️⃣ **Environmental Score (Optional)** – Adjusts based on an organization's unique environment.  

#### **4. Example: CVSS Calculation**  
📌 **Example Vulnerability: CVE-2021-44228 (Log4Shell)**  
- **Attack Vector:** Network (AV:N) → Can be exploited remotely.  
- **Attack Complexity:** Low (AC:L) → Easy to execute.  
- **Privileges Required:** None (PR:N) → No authentication needed.  
- **User Interaction:** None (UI:N) → No user action required.  
- **Confidentiality, Integrity, Availability:** High (C:H/I:H/A:H) → Complete compromise.  

✅ **CVSS Score: 10.0 (Critical)**  

#### **5. Where to Check CVSS Scores?**  
- **NVD (National Vulnerability Database):** [https://nvd.nist.gov/](https://nvd.nist.gov/)  
- **CVSS Calculator:** [https://www.first.org/cvss/calculator/3.1](https://www.first.org/cvss/calculator/3.1)  

#### **6. How CVSS Helps in SCA?**  
- SCA tools (**Snyk, OWASP Dependency-Check, Black Duck**) use CVSS scores to **prioritize vulnerabilities**.  
- Higher CVSS = **Faster remediation required**.  
- Used in **risk management and compliance** (PCI DSS, ISO 27001).  

### **Why CVSS Matters?**  
✔️ Helps **prioritize vulnerabilities** based on severity.  
✔️ Used globally for **security risk assessment**.  
✔️ Standardized across all industries.  
