## 📌 Insecure Deserialization 
🔹 What is Serialization & Deserialization? <br>
**Serialization** = Converting **objects** into **data (text or binary)** to store or send. <br>
**Deserialization** = Converting **data** back into **objects** to use in a program.

📌 What is Insecure Deserialization?

Insecure deserialization occurs when an application deserializes untrusted data without proper validation, allowing an attacker to modify objects and potentially execute arbitrary code or escalate privileges. This can lead to remote code execution (RCE), privilege escalation, data tampering, and denial of service (DoS).

🚨 Impact: <br>
✅ Remote Code Execution (RCE) <br>
✅ Authentication Bypass <br>
✅ Privilege Escalation <br>
✅ Data Tampering


### **Insecure Deserialization**
Insecure deserialization is a vulnerability that occurs when an application deserializes untrusted or manipulated data without proper validation, leading to security risks such as remote code execution, privilege escalation, and data tampering.

### **How It Works**
1. **Serialization:** The process of converting an object into a format (e.g., JSON, XML, or binary) that can be stored or transmitted.
2. **Deserialization:** The process of converting the stored format back into an object.
3. **Exploitation:** Attackers modify serialized data to inject malicious payloads, which can execute unintended commands upon deserialization.

### **Common Exploits**
- **Remote Code Execution (RCE):** Attackers inject malicious code into serialized objects.
- **Privilege Escalation:** Altering object properties to gain higher privileges.
- **Data Tampering:** Modifying application logic by changing object properties.
- **Denial of Service (DoS):** Creating large or corrupted objects to crash the system.


### **Examples**
#### **1. Java Deserialization Attack (Using `readObject()`)**
Many Java applications use **ObjectInputStream** to deserialize objects. Attackers can craft malicious serialized objects to execute arbitrary code. <br>
```java
ObjectInputStream in = new ObjectInputStream(socket.getInputStream());
MyObject obj = (MyObject) in.readObject(); // Untrusted deserialization
```
If an attacker controls the input, they can send a malicious serialized object that executes arbitrary code.

#### **Solution 1: Use a Secure Deserialization Library**
Instead of standard `ObjectInputStream`, use **Apache Commons-IO’s ValidatingObjectInputStream** to allow only trusted classes:

```java
import org.apache.commons.io.serialization.ValidatingObjectInputStream;
import java.io.InputStream;

InputStream inputStream = socket.getInputStream();
ValidatingObjectInputStream in = new ValidatingObjectInputStream(inputStream);

// Whitelist allowed classes
in.accept(MyObject.class);

MyObject obj = (MyObject) in.readObject(); // Secure deserialization
```

🔹 This approach ensures that only expected classes can be deserialized.

#### **Solution 2: Use JSON or XML Instead**
Instead of Java serialization, use safer data formats like **JSON** with libraries like Jackson or Gson:

**Using Jackson:**
```java
import com.fasterxml.jackson.databind.ObjectMapper;
import java.io.InputStream;

ObjectMapper objectMapper = new ObjectMapper();
MyObject obj = objectMapper.readValue(socket.getInputStream(), MyObject.class);
```
🔹 JSON is safer because it doesn’t support direct execution of methods.

---

#### **2. PHP Unserialize Attack**
In PHP, the `unserialize()` function can be exploited if used on user-controlled data.
```php
$data = $_GET['data']; 
$object = unserialize($data); // Dangerous if $data is untrusted
```
An attacker can craft a malicious object in serialized form to exploit application logic.

#### **Solution 1: Use `json_decode()` Instead of `unserialize()`**
Since JSON doesn’t support direct object execution, it's a safer alternative:

```php
$data = $_GET['data']; 
$object = json_decode($data, true); // Secure JSON decoding
```

🔹 **Why safer?** Unlike `unserialize()`, JSON cannot instantiate PHP objects automatically.

#### **Solution 2: Use a Whitelist (`allowed_classes`)**
If deserialization is necessary, restrict it to safe classes using **`unserialize()` with `allowed_classes`**:

```php
$data = $_GET['data']; 
$allowed_classes = ['SafeClass']; // Only allow specific classes
$object = unserialize($data, ['allowed_classes' => $allowed_classes]);
```

🔹 This prevents attackers from injecting arbitrary objects into the system.

---

### **Final Takeaways**
✅ Avoid native deserialization (unserialize() in PHP, ObjectInputStream in Java).
✅ Use safer formats like JSON instead of serialized objects.
✅ If deserialization is required, whitelist allowed classes.
✅ Monitor and log deserialization attempts for anomalies.

Would you like a hands-on example for testing these fixes? 🚀



### **How to Prevent Insecure Deserialization**
1. **Use Safe Data Formats:** Prefer safer serialization formats like **JSON or XML** over native language-specific formats.
2. **Implement Data Integrity Checks:** Use **signatures, hashes, or encryption** to detect tampering.
3. **Whitelist Acceptable Classes:** Restrict deserialization to known, safe classes.
4. **Use Sandboxing:** Run deserialization in a restricted environment.
5. **Monitor and Log Deserialization Attempts:** Detect and block suspicious activities.
6. **Disable Unnecessary Deserialization Features:** If deserialization is not required, disable it.
