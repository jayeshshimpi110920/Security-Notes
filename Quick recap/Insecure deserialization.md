## 📌 Insecure Deserialization 
🔹 What is Serialization & Deserialization? <br>
**Serialization** = Converting **objects** into **data (text or binary)** to store or send. <br>
**Deserialization** = Converting **data** back into **objects** to use in a program.

📌 What is Insecure Deserialization?

Insecure deserialization occurs when an application deserializes untrusted data without proper validation, allowing an attacker to modify objects and potentially execute arbitrary code or escalate privileges.

🚨 Impact: <br>
✅ Remote Code Execution (RCE) <br>
✅ Authentication Bypass <br>
✅ Privilege Escalation <br>
✅ Data Tampering


