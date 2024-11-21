### Buffer Overflow in SAST (Static Application Security Testing)

A **buffer overflow** occurs when a program writes more data to a buffer (memory space) than it can hold, potentially leading to undefined behavior, crashes, or exploitation.
That extra data overflows into adjacent memory locations and corrupts or overwrites the data in those locations.

---

### **Example Code**:

#### Before Mitigation (Vulnerable Code):
```c
#include <stdio.h>
#include <string.h>

void vulnerableFunction(char *input) {
    char buffer[10];  // Fixed-size buffer
    strcpy(buffer, input);  // No bounds checking
    printf("Buffer content: %s\n", buffer);
}

int main() {
    char input[20] = "ThisIsTooLongForBuffer";
    vulnerableFunction(input);
    return 0;
}
```

- **Issue**: `strcpy()` copies data into the buffer without checking its size, causing an overflow if the input exceeds 10 characters.

---

#### After Mitigation (Secure Code):
```c
#include <stdio.h>
#include <string.h>

void secureFunction(char *input) {
    char buffer[10];  // Fixed-size buffer
    strncpy(buffer, input, sizeof(buffer) - 1);  // Bounds checking
    buffer[sizeof(buffer) - 1] = '\0';  // Null-terminate the string
    printf("Buffer content: %s\n", buffer);
}

int main() {
    char input[20] = "ThisIsTooLongForBuffer";
    secureFunction(input);
    return 0;
}
```

- **Fix**: `strncpy()` ensures the copied string doesn't exceed the buffer size and prevents overflow.

---

### **Prevention Strategies**:

1. **Input Validation**:
   - Validate input lengths before copying to buffers.
   
2. **Use Safer Functions**:
   - Replace unsafe functions (`strcpy`, `gets`, etc.) with safer alternatives like `strncpy`, `fgets`, and `snprintf`.

3. **Bounds Checking**:
   - Always check array or buffer sizes before writing data.

4. **Use Dynamic Memory**:
   - Allocate memory dynamically based on the required size to avoid fixed-size buffers.

5. **Enable Compiler Protections**:
   - Use features like stack canaries (`-fstack-protector` in GCC), Address Space Layout Randomization (ASLR), and memory safety tools.

6. **Use Modern Languages**:
   - Prefer memory-safe languages like Python, Java, or Rust, which manage memory safely.

---

### **Impact of Buffer Overflow**:

1. **System Crashes**:
   - Application termination or instability.

2. **Unauthorized Access**:
   - Allows attackers to overwrite critical data or inject malicious code.

3. **Arbitrary Code Execution**:
   - Exploits can lead to the execution of attacker-controlled instructions.

4. **Data Corruption**:
   - Overflows can modify application data, leading to unintended behavior.

5. **Denial of Service (DoS)**:
   - Exhausting system resources or crashing the program.

---

### **Manual Source Code Review for Buffer Overflow**:

1. **Identify Unsafe Functions**:
   - Look for functions like `strcpy`, `gets`, `sprintf`, `scanf`, and others without proper bounds checking.

2. **Check Buffer Size Declarations**:
   - Verify that buffers are appropriately sized for the expected input.

3. **Trace Input Sources**:
   - Follow the data flow of user inputs to ensure size checks exist.

4. **Examine Loops**:
   - Ensure loops that write to buffers have boundary conditions.

5. **Review Error Handling**:
   - Check for cases where unexpected inputs might bypass validations.

6. **Dynamic Analysis**:
   - If possible, combine static analysis with fuzz testing or runtime debugging tools like Valgrind.

---

### **Best Practices to Avoid Buffer Overflow**:

1. **Avoid Fixed-Size Buffers**:
   - Use dynamically allocated memory whenever possible.

2. **Use Modern Libraries**:
   - Libraries like Safe C Library (`safeclib`) can help mitigate vulnerabilities.

3. **Educate Developers**:
   - Train developers on secure coding practices.

4. **Leverage SAST Tools**:
   - Use tools like Coverity, Fortify, or Checkmarx to automate detection.

5. **Implement Secure Coding Standards**:
   - Follow guidelines such as CERT C Secure Coding Standards.
