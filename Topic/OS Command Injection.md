## OS Command Injection
OS command injection is a critical vulnerability that occurs when an attacker is able to execute arbitrary operating system commands on a server or system due to improper input validation in a web application or system. This vulnerability typically arises when user-supplied input is directly incorporated into system-level commands without proper sanitization. 
POV : Command Injection: This occurs when an attacker can inject system commands through web forms or parameters, allowing them to execute commands on the server.

### Common Scenarios
* Web Applications: If an application accepts user input and passes it to system commands (e.g., through shell commands or scripts), and if the input is not properly validated or sanitized, an attacker can append malicious commands.

* Command-Line Utilities: Applications using command-line utilities like ping, nslookup, or netstat that directly take user input can be exploited to inject OS commands.

> $ip = $_GET['ip']; <br>
  // Vulnerable code <br>
  **exec**("ping " . $ip);

Here, if the input is not sanitized, an attacker could pass something like:
> 127.0.0.1; rm -rf / # This would delete the server's root directory

### Key Impact
- **System Takeover**: Execution of arbitrary commands can lead to full control of the system.
- **Data Exfiltration**: Attackers can extract sensitive files or credentials.
- **Denial of Service (DoS)**: Critical system files can be deleted or altered, making the system unusable.

### Mitigation Strategies

1. **Input Validation and Sanitization**:
   - Always validate and sanitize user inputs.
   - Use whitelisting techniques where only expected inputs (like IP addresses or domain names) are allowed.

2. **Use of Built-in APIs**:
   - Instead of directly invoking system commands, use high-level APIs provided by the programming language or framework that abstract system calls.

3. **Parameterized Commands**:
   - Similar to parameterized queries in SQL injection, use libraries that allow you to safely pass parameters to OS commands without directly concatenating user input.

4. **Least Privilege**:
   - Ensure the application runs with minimal system privileges, reducing the impact of successful exploitation.

5. **Command Escaping**:
   - Use functions that automatically escape user input when passed to system commands (e.g., `escapeshellcmd()` in PHP).

### Tools for Detection
- **Burp Suite**: You can test for command injection vulnerabilities by injecting special characters like `;`, `&&`, `|`, and variations of OS commands into input fields, observing the application's response.
- **OWASP ZAP**: Used for automated scanning, including command injection vulnerability detection.

---
## Identification
Look for **input fields** where user-supplied data might be passed to system commands, such as a **form** for executing a (ping or traceroute, file uploads, or search functionality).
Once identified a possible vulnerabilitiy, send burpsuite request to repeater tab, and modify the request and send it multiple times to observe how the server responds.

---
### Common Payload to try :
Modify the input fields in the request to inject command sequences that could reveal if the system is vulnerable to command injection.

Linux/Unix-based system
> ; ls -la <br>
| id <br>
&& whoami <br>
; cat /etc/passwd <br>

Window-based system:
> | dir <br>
& whoami <br>
; type C:\Windows\System32\drivers\etc\hosts
















