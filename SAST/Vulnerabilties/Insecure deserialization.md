## Insecure Deserialization
Insecure Deserialization occurs when untrusted data is deserialized (converted from a serialized format to an object) without proper validation. This vulnerability allows attackers to manipulate serialized data to execute arbitrary code, gain unauthorized access, or tamper with application logic.


Here’s a **simplified** example of insecure deserialization and its mitigation:

### **Vulnerable Code (Insecure Deserialization)**

This is a basic example of a vulnerable code snippet where untrusted data is deserialized:

```java
import java.io.*;

public class InsecureDeserializationExample {
    public static void main(String[] args) throws Exception {
        // Deserialize an object from an untrusted source (user input, file, etc.)
        ObjectInputStream ois = new ObjectInputStream(new FileInputStream("data.ser"));
        Object obj = ois.readObject();  // Insecure: Data can be manipulated by attackers
        ois.close();
        
        // Use the deserialized object
        System.out.println(obj);
    }
}
```

#### **Attack Scenario:**
An attacker can modify the `data.ser` file to include malicious data that, when deserialized, could lead to code execution or other exploits.

### **Mitigated Code (Secure Deserialization)**

To mitigate this, we can restrict the types of objects that can be deserialized and avoid deserializing untrusted data.

```java
import java.io.*;

public class SecureDeserializationExample {
    public static void main(String[] args) throws Exception {
        // Custom deserialization: only allow specific classes
        ObjectInputStream ois = new ObjectInputStream(new FileInputStream("data.ser")) {
            @Override
            protected Class<?> resolveClass(ObjectStreamClass desc) throws IOException, ClassNotFoundException {
                // Allow only the trusted User class to be deserialized
                if (desc.getName().equals("User")) {
                    return super.resolveClass(desc);
                } else {
                    throw new InvalidClassException("Unauthorized deserialization attempt");
                }
            }
        };
        
        Object obj = ois.readObject();  // Safe: Only allowed classes are deserialized
        ois.close();
        
        // Use the deserialized object
        System.out.println(obj);
    }
}
```

#### **Key Points of Mitigation:**
1. **Custom `resolveClass` Method**: Only deserializes objects of trusted types (e.g., `User` class).
2. **Avoid Deserializing Untrusted Data**: Ensure you only deserialize data from trusted sources.

By using this approach, attackers cannot inject malicious classes or payloads during deserialization.


How to prevent insecure deserialization:
---
To **prevent insecure deserialization**, you can implement several best practices to ensure that serialized data is handled safely. Here's a step-by-step guide on how to prevent it:

### 1. **Avoid Deserializing Untrusted Data**
   - **Don't deserialize data from untrusted or unknown sources** (e.g., user input, files, or external systems) unless absolutely necessary.
   - **Only deserialize data from trusted sources** (e.g., internal systems, verified files).

### 2. **Use Safe Serialization Formats**
   - **Use JSON, XML, or other human-readable formats** instead of binary serialization (e.g., Java's default `ObjectInputStream`).
   - **These formats are less prone to exploits** and can be validated more easily before processing.

### 3. **Limit the Classes That Can Be Deserialized**
   - **Restrict which classes can be deserialized**. You can customize the deserialization process to check if the class being deserialized is from a trusted set of classes.
   
   Example in Java:
   ```java
   class SecureObjectInputStream extends ObjectInputStream {
       public SecureObjectInputStream(InputStream in) throws IOException {
           super(in);
       }

       @Override
       protected Class<?> resolveClass(ObjectStreamClass desc) throws IOException, ClassNotFoundException {
           // Allow only trusted classes
           if (desc.getName().equals("com.myapp.User")) {
               return super.resolveClass(desc);
           } else {
               throw new InvalidClassException("Unauthorized deserialization attempt");
           }
       }
   }
   ```

### 4. **Sign and Encrypt Serialized Data**
   - **Sign serialized data** to ensure its integrity and authenticity, so any tampering is easily detectable.
   - **Encrypt serialized data** to prevent unauthorized access or modification.
   - For example, **digital signatures** or **HMAC (Hash-based Message Authentication Code)** can be used to verify the integrity of the serialized data.

### 5. **Use Safe Libraries for Serialization**
   - **Avoid using unsafe serialization libraries** like Java's `ObjectInputStream` and `ObjectOutputStream`.
   - Use libraries designed to safely handle data formats like JSON (e.g., Jackson, Gson), XML, or Protocol Buffers.

### 6. **Implement Integrity Checks**
   - Add checks such as **checksums** or **hashes** to verify that the serialized data has not been tampered with.
   - Before deserialization, you can check the integrity of the serialized object by comparing the hash value or signature with a pre-generated one.

### 7. **Disable Deserialization Features in Frameworks**
   - If using a framework or platform that performs deserialization, **disable or restrict unsafe deserialization features**.
   - For example, disable or filter **remote code execution (RCE)** triggers when handling deserialization in frameworks like Apache Commons Collections, or ensure you are using safe serialization versions.

### 8. **Use Object Whitelisting**
   - **Whitelist classes** that can be deserialized. Only deserialize objects of known, safe types.
   - For example, use code that checks the class type before proceeding with deserialization:
   ```java
   if (obj instanceof User) {
       // Proceed with trusted object
   } else {
       throw new InvalidClassException("Unsafe object type");
   }
   ```

### 9. **Monitor and Log Deserialization Activities**
   - Log any deserialization actions and monitor for unusual or unexpected deserialization attempts.
   - This helps to detect abnormal or suspicious behavior in production environments.

### 10. **Update and Patch Libraries**
   - Ensure that any libraries or frameworks you use for deserialization are up to date and do not contain known vulnerabilities.
   - Regularly patch vulnerabilities related to deserialization in dependencies.

---

### **Summary of Key Prevention Methods**:
- **Avoid deserializing untrusted data**.
- **Use safe formats (JSON, XML)** instead of binary serialization.
- **Restrict the types of objects that can be deserialized**.
- **Sign and encrypt serialized data** to prevent tampering.
- **Use safe, trusted libraries** for serialization.
- **Implement integrity checks** and **monitor deserialization activities**.
- **Keep frameworks and libraries up-to-date**.

By applying these practices, you can significantly reduce the risk of insecure deserialization and improve the security of your applications.

