# SQL injection  --
### **Real-World Scenario (Before Mitigation)**  
Imagine a web application with a login feature where the SQL query directly concatenates user input. This creates a SQL injection vulnerability.

#### **Vulnerable Code** (Before Mitigation)  
```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.Statement;

public class Login {
    public static boolean authenticate(String username, String password) {
        boolean isAuthenticated = false;
        try {
            Connection conn = DriverManager.getConnection(
                "jdbc:mysql://localhost:3306/mydb", "root", "password");
            Statement stmt = conn.createStatement();
            
            // Vulnerable query
            String query = "SELECT * FROM users WHERE username = '" 
                           + username + "' AND password = '" + password + "'";
            ResultSet rs = stmt.executeQuery(query);
            
            if (rs.next()) {
                isAuthenticated = true; // User exists
            }
            conn.close();
        } catch (Exception e) {
            e.printStackTrace();
        }
        return isAuthenticated;
    }
    
    public static void main(String[] args) {
        String username = "admin' -- ";  // Malicious input
        String password = "anything";
        if (authenticate(username, password)) {
            System.out.println("Login successful!");
        } else {
            System.out.println("Login failed!");
        }
    }
}
```

#### **Why is this vulnerable?**
- The SQL query concatenates user input directly, allowing an attacker to inject malicious SQL.
- Malicious input (`admin' --`) changes the query to:
  ```sql
  SELECT * FROM users WHERE username = 'admin' -- ' AND password = 'anything'
  ```
  - The `--` comments out the rest of the query, bypassing authentication.

### **Mitigated Code (After Fixing the Vulnerability)**  
Using **Prepared Statements** eliminates the risk by parameterizing input.

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;

public class Login {
    public static boolean authenticate(String username, String password) {
        boolean isAuthenticated = false;
        try {
            Connection conn = DriverManager.getConnection(
                "jdbc:mysql://localhost:3306/mydb", "root", "password");
            
            // Secure query using prepared statements
            String query = "SELECT * FROM users WHERE username = ? AND password = ?";
            PreparedStatement pstmt = conn.prepareStatement(query);
            pstmt.setString(1, username); // Parameterized input
            pstmt.setString(2, password);
            
            ResultSet rs = pstmt.executeQuery();
            if (rs.next()) {
                isAuthenticated = true; // User exists
            }
            conn.close();
        } catch (Exception e) {
            e.printStackTrace();
        }
        return isAuthenticated;
    }
    
    public static void main(String[] args) {
        String username = "admin";
        String password = "securepassword";
        if (authenticate(username, password)) {
            System.out.println("Login successful!");
        } else {
            System.out.println("Login failed!");
        }
    }
}
```

### **Mitigations Implemented:**
1. **Use of Prepared Statements:**  
   - Input parameters are bound to placeholders (`?`) in the SQL query.
   - Prevents execution of malicious SQL.

2. **Input Validation:**  
   - Sanitize inputs to allow only expected characters (e.g., alphanumerics for usernames).

3. **Database Permissions:**  
   - Use a restricted database user for the application with limited privileges (e.g., no `DROP` or `ALTER` access).

4. **Use of ORM (Optional):**  
   - Tools like Hibernate abstract SQL handling, making it harder to inject SQL.

### **Testing**
- **Vulnerable Code:** Enter `admin' --` as the username and observe unauthorized access.  
- **Fixed Code:** The same input results in a failed login because the query treats `admin' --` as a literal string.

---
# Command Injection - 

### **Real-World Scenario (Before Mitigation)**  
Imagine a web application that allows users to ping an IP address. The application uses user input in a system command without proper sanitization, leading to command injection.

#### **Vulnerable Code (Before Mitigation)**  
```java
import java.io.BufferedReader;
import java.io.InputStreamReader;

public class PingUtility {
    public static void ping(String ipAddress) {
        try {
            // Vulnerable: Directly incorporating user input into the command
            String command = "ping -c 4 " + ipAddress;
            Process process = Runtime.getRuntime().exec(command);

            BufferedReader reader = new BufferedReader(
                new InputStreamReader(process.getInputStream()));
            String line;
            while ((line = reader.readLine()) != null) {
                System.out.println(line);
            }
            process.waitFor();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    public static void main(String[] args) {
        String userInput = "127.0.0.1; rm -rf /"; // Malicious input
        ping(userInput);
    }
}
```

#### **Why is this vulnerable?**
- The user input (`127.0.0.1; rm -rf /`) is directly concatenated into the command:
  ```bash
  ping -c 4 127.0.0.1; rm -rf /
  ```
- The semicolon (`;`) allows execution of multiple commands, enabling the attacker to delete files or execute arbitrary code.

---

### **Mitigated Code (After Fixing the Vulnerability)**  

Using strict input validation and safer methods to execute system commands.

```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.util.regex.Pattern;

public class PingUtility {
    public static void ping(String ipAddress) {
        try {
            // Validate input to allow only valid IP addresses
            if (!isValidIPAddress(ipAddress)) {
                throw new IllegalArgumentException("Invalid IP address");
            }

            // Secure: Avoid concatenating user input in the command
            ProcessBuilder processBuilder = new ProcessBuilder("ping", "-c", "4", ipAddress);
            Process process = processBuilder.start();

            BufferedReader reader = new BufferedReader(
                new InputStreamReader(process.getInputStream()));
            String line;
            while ((line = reader.readLine()) != null) {
                System.out.println(line);
            }
            process.waitFor();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    // Validate input: Ensure only valid IPv4/IPv6 addresses are allowed
    private static boolean isValidIPAddress(String ip) {
        String ipv4Pattern = "^((25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\\.){3}(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)$";
        String ipv6Pattern = "^[0-9a-fA-F:]+$"; // Simplified IPv6 regex
        return Pattern.matches(ipv4Pattern, ip) || Pattern.matches(ipv6Pattern, ip);
    }

    public static void main(String[] args) {
        String userInput = "127.0.0.1"; // Safe input
        ping(userInput);
    }
}
```

### **Mitigations Implemented:**

1. **Input Validation:**  
   - Validate user input against expected formats (e.g., valid IPv4/IPv6 addresses) using regex.

2. **Avoid Direct Concatenation:**  
   - Use `ProcessBuilder` or equivalent APIs to handle arguments safely without concatenating input.

3. **Least Privilege:**  
   - Run the application with minimal privileges to limit the damage of potential exploits.

4. **Escape User Input (if necessary):**  
   - When user input must be passed to shell commands, escape special characters to neutralize injection (though avoiding direct shell invocation is preferred).

### **Testing the Fix**
- **Vulnerable Code:** Input `127.0.0.1; rm -rf /` executes the `ping` command and deletes files.  
- **Fixed Code:** Malicious input results in an `IllegalArgumentException`, preventing command execution.

### List of Dangerous Commands/Functions for Command Injection (General)

1. **`exec()`**  
   Executes commands or code dynamically.

2. **`system()`**  
   Executes shell commands.

3. **`popen()`**  
   Opens a pipe to a process for communication.

4. **`passthru()`**  
   Executes a command and outputs raw results.

5. **`eval()`**  
   Evaluates strings as code or expressions.

6. **`shell_exec()`**  
   Executes shell commands and returns output as a string.

7. **`proc_open()`**  
   Executes a command and opens a process.

8. **`backticks` (`` `command` ``)**  
   Executes a shell command and captures its output.

9. **`spawn()`**  
   Spawns a new process to execute a command.

10. **`execve()`**  
    Replaces the current process with a new process.

11. **`fork()` and `exec()` together**  
    Creates a new process and executes a command within it.

12. **`os.system()`**  
    Runs a system command in Python.

13. **`subprocess.Popen()`**  
    Starts a new process for a command in Python.

14. **`Runtime.getRuntime().exec()`**  
    Executes commands in Java.

15. **`ProcessBuilder.start()`**  
    Builds and starts a process to execute commands in Java.

16. **`cmd.exe` / `sh`**  
    Used to execute shell commands directly.

17. **`open()` (for devices or files like `/dev/tcp`)**  
    Opens files or special devices to execute operations.

18. **`sudo`**  
    Runs commands with elevated privileges, potentially escalating risks.

19. **`perl` / `ruby` / `python` command-line invocations**  
    Executes code or commands within these interpreters.

20. **`PowerShell Invoke-Expression`**  
    Dynamically executes a string as PowerShell commands.

21. **`perl -e` / `python -c` / `ruby -e`**  
    Allows inline execution of code snippets.

22. **`nc` (Netcat)**  
    Used to open reverse shells or send arbitrary commands over a network.

23. **`curl` / `wget`**  
    Can fetch and execute remote scripts or commands.

24. **`load_file()` / `load data infile`**  
    Database commands that can load files and execute contents.

25. **`sh` / `bash` (via scripts or direct calls)**  
    Executes arbitrary shell scripts or commands.

### **Best Practices to Avoid Risks**:
1. Avoid using these commands unless absolutely necessary.
2. Validate and sanitize all inputs strictly.
3. Use safe alternatives like libraries or APIs for specific tasks.
4. Employ **least privilege** principles to limit access.
5. Monitor logs and restrict access to vulnerable functionalities.

---

# Code injection and command injection :

**Code Injection** and **Command Injection** are both types of injection vulnerabilities but differ in their targets, execution methods, and impacts. Here's a comparison:

### **Code Injection**
1. **Target**  
   Injects malicious code into the application's codebase or execution environment.

2. **Execution Context**  
   - The injected code is interpreted or executed by the application's programming environment (e.g., Python, PHP, Java).
   - It exploits application-level vulnerabilities.

3. **Scope**  
   - Impacts the application directly.
   - Can lead to unauthorized operations, data theft, or remote code execution.

4. **Example**  
   - **PHP Code Injection**:  
     ```php
     eval($_GET['code']); // Input: `echo system('ls');`
     ```
   - The attacker can inject and execute arbitrary PHP code.

5. **Mitigation**  
   - Avoid functions like `eval`, `exec`, or dynamic code interpretation.
   - Validate and sanitize all inputs.
   - Use secure coding frameworks.


### **Command Injection**
1. **Target**  
   Injects malicious commands to be executed at the operating system (OS) level.

2. **Execution Context**  
   - The injected commands are executed by the operating system shell (e.g., bash, cmd).
   - It exploits system-level vulnerabilities or interfaces.

3. **Scope**  
   - Impacts the underlying server or system hosting the application.
   - Can lead to system compromise, file deletion, or privilege escalation.

4. **Example**  
   - **Shell Command Injection**:  
     ```php
     system("ping " . $_GET['ip']); // Input: `127.0.0.1; rm -rf /`
     ```
   - The attacker can inject shell commands to delete files or compromise the system.

5. **Mitigation**  
   - Avoid passing unsanitized user input to system commands.
   - Use APIs or libraries that interact directly with the OS without invoking shell commands (e.g., `Python subprocess.run` with strict argument handling).


### **Key Differences**

| Aspect                | Code Injection                             | Command Injection                        |
|-----------------------|--------------------------------------------|------------------------------------------|
| **Execution**         | Application-level (code interpreted by app)| System-level (commands executed by OS)   |
| **Impact**            | Affects application behavior or logic      | Affects server or system operations      |
| **Example Target**    | PHP `eval`, Python `exec`                  | Shell commands (`ls`, `rm`, `ping`)      |
| **Severity**          | Limited to app vulnerabilities             | Can compromise the entire system         |

---

In summary, **Code Injection** compromises the application logic by injecting code into the app's runtime, while **Command Injection** targets the operating system by executing malicious system commands. Both are dangerous, but Command Injection generally poses a higher risk due to its ability to control the underlying system.
