### Encryption vs. Hashing Cheat Sheet
### 1. **Encryption**

- **Purpose**: Convert readable data (plaintext) into an unreadable form (ciphertext) to protect it from unauthorized access.
- **Process**: Uses an encryption algorithm and a key to transform plaintext into ciphertext.
- **Types**: 
  1. **Symmetric Encryption**: Same key is used for both encryption and decryption.
     - **Examples**: AES, DES, 3DES.
  2. **Asymmetric Encryption**: Uses a pair of keys, one for encryption (public key) and one for decryption (private key).
     - **Examples**: RSA, ECC.

- **Key Characteristics**:
  - **Reversible**: The original data can be restored using the key (decryption).
  - **Use Case**: Protecting data during transmission (TLS/SSL), encrypting files, securing communications.

- **Examples of Use**:
  - **Transport Layer Security (TLS)**: Secures communication over a network.
  - **File Encryption**: Protects sensitive data on disk.

## 2. **Hashing**

- **Purpose**: Generate a fixed-size output (hash) from input data, which is unique to the input. Used to verify integrity and securely store data (like passwords).
- **Process**: A hash function takes input and produces a unique fixed-size string, usually represented as a hexadecimal number.
- **Popular Hashing Algorithms**: 
  1. **MD5**: Produces a 128-bit hash value (no longer considered secure).
  2. **SHA-1**: Produces a 160-bit hash value (deprecated due to vulnerabilities).
  3. **SHA-256**: Part of the SHA-2 family, more secure than MD5 and SHA-1.

- **Key Characteristics**:
  - **Irreversible**: Once data is hashed, it cannot be converted back to its original form.
  - **Deterministic**: The same input will always produce the same hash.
  - **Collision Resistance**: It should be hard to find two different inputs that produce the same hash (though this can be compromised in weak algorithms like MD5).

- **Examples of Use**:
  - **Password Storage**: Hash passwords before storing them in a database to prevent exposure of plain-text passwords.
  - **Data Integrity**: Ensure that data has not been tampered with (e.g., digital signatures, file integrity checks).

## 3. **Key Differences**

| Feature                  | Encryption                          | Hashing                                 |
|--------------------------|--------------------------------------|-----------------------------------------|
| **Purpose**               | Protect confidentiality of data     | Ensure integrity, used for verification |
| **Reversible**            | Yes (with the right key)            | No                                     |
| **Key Usage**             | Requires a key for decryption       | No keys involved                        |
| **Common Algorithms**     | AES, RSA, DES                       | SHA-256, SHA-3, MD5                    |
| **Output Length**         | Variable based on the algorithm     | Fixed output size (e.g., 256 bits for SHA-256) |
| **Use Case**              | Protect data (e.g., in transit)     | Verify data integrity (e.g., passwords, file checks) |

## 4. **Advanced Concepts**

### **Salting (for Hashing)**
- **Explanation**: Adding a unique, random value to a password before hashing it. This ensures that even if two users have the same password, their hashes will be different.
- **Use Case**: Commonly used in password storage to prevent rainbow table attacks.

### **Pepper (for Hashing)**
- **Explanation**: A secret value added to a hash that is not stored alongside the hash but is known by the server. Adds an extra layer of protection.

### **Digital Signatures**
- **Explanation**: Uses asymmetric encryption to verify the integrity and authenticity of a message. The sender encrypts the hash of a message with their private key, and the recipient decrypts it with the sender's public key.
- **Use Case**: Signing emails, software distribution, digital contracts.

### **Hashing vs. Encryption Use Cases**
- **Encryption**: Use when you need to send sensitive data securely (e.g., encrypting a message or file).
- **Hashing**: Use when you need to verify that data has not been altered (e.g., verifying a password or file integrity).

## 5. **Where We Use Hashing and Encryption**

### **Use Cases for Hashing**
Hashing is primarily used in scenarios where data integrity and authentication are critical. Here are some common use cases:

1. **Password Storage**:
   - Hashes are generated for user passwords and stored in databases to prevent exposure of plain-text passwords.
   - **Salting** is often used to ensure that identical passwords do not generate the same hash.

2. **Data Integrity Verification**:
   - Hash functions are used to generate checksums or hash values for files. When files are transferred or stored, the hash can be recalculated to verify that the data has not been altered.
   - Common in software distribution to ensure that the downloaded files are authentic and untampered.

3. **Digital Signatures**:
   - Hashing is used to create a hash of a message that is then encrypted with a private key to create a digital signature. This ensures that the message has not been altered in transit and verifies the sender's identity.

4. **File Deduplication**:
   - Hashing is used to identify duplicate files in storage systems. By hashing file content, systems can determine if files are identical without comparing the content directly.

5. **API Keys and Tokens**:
   - Hashing can be used to securely store API keys or tokens to avoid direct exposure of sensitive credentials.

### **Use Cases for Encryption**
Encryption is used to secure data confidentiality during transmission or storage. Here are some common use cases:

1. **Data Transmission**:
   - Secure communication over the internet is achieved using protocols like TLS/SSL, which encrypt data to protect it from eavesdropping.
   - **Examples**: HTTPS, email encryption (PGP, S/MIME).

2. **File Encryption**:
   - Sensitive files stored on disks or cloud services can be encrypted to prevent unauthorized access.
   - **Examples**: Encrypting hard drives using BitLocker or FileVault.

3. **Database Encryption**:
   - Data stored in databases can be encrypted to protect sensitive information such as personally identifiable information (PII) or financial data.
   - **Examples**: Transparent Data Encryption (TDE) in SQL Server or Oracle.

4. **Secure Messaging**:
   - Messaging apps often use end-to-end encryption to ensure that only the communicating users can read the messages.
   - **Examples**: Signal, WhatsApp, and Telegram.

5. **VPNs (Virtual Private Networks)**:
   - VPNs encrypt data transmitted over public networks to ensure secure communication and privacy for users.
   - **Examples**: OpenVPN, IPSec, WireGuard.

6. **Email Encryption**:
   - Emails can be encrypted to protect sensitive information from being intercepted during transmission.
   - **Examples**: PGP (Pretty Good Privacy), S/MIME (Secure/Multipurpose Internet Mail Extensions).

## 6. **Summary**
- **Hashing** is primarily used for verifying data integrity, storing passwords securely, and ensuring that files have not been altered.
- **Encryption** is used to protect the confidentiality of sensitive data during transmission and storage, ensuring that only authorized parties can access the information.

Understanding these use cases will help you identify when to use hashing versus encryption based on the specific security requirements of your application or system.
