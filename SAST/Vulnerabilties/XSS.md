##  Reflected Cross-Site Scripting (XSS)

Vulnerability Code (Before Mitigation)
```
<!-- Vulnerable code rendering user input without escaping -->
<div>Hello, <%= request.getParameter("username") %></div>
```
Code After Mitigation
```
<!-- Mitigated code with input sanitization -->
<%@ taglib uri="http://www.springframework.org/tags" prefix="spring" %>
<div>Hello, <%= HtmlUtils.htmlEscape(request.getParameter("username")) %></div>
```
SAST Output
```
Issue: Reflected XSS Vulnerability
File: /app/src/DisplayPage.jsp
Line: 109
Description: User input from the query string is rendered directly onto the page without escaping, which can lead to reflected cross-site scripting (XSS) attacks.
Recommendation: Ensure user input is sanitized or escaped before being inserted into the HTML page.
Example Fix: 
    String safeUsername = HtmlUtils.htmlEscape(request.getParameter("username"));
    out.println("<h1>Hello, " + safeUsername + "</h1>");
```

---
Yes, the code snippet you provided is potentially vulnerable to **Cross-Site Scripting (XSS)** attacks. Specifically, it's an example of **Reflective XSS**.

Here’s why:

```jsp
<div>Hello, <%= request.getParameter("username") %></div>
```

### How it works:
- The server takes a `username` parameter from the HTTP request, and directly embeds it into the HTML output.
- If the `username` parameter is controlled by an attacker and they provide malicious JavaScript code as the value (e.g., `<script>alert('XSS')</script>`), this script will be executed in the user's browser when the page is rendered.

### Example of XSS in action:
If an attacker sends a request like:

```
http://example.com/welcome.jsp?username=<script>alert('XSS')</script>
```

The response would include:

```html
<div>Hello, <script>alert('XSS')</script></div>
```

This would execute the JavaScript code and trigger the alert box.

### How to prevent this:
To avoid XSS vulnerabilities, you should **escape** the user input before embedding it into the HTML page. In Java, you can use `org.apache.commons.text.StringEscapeUtils` or `ESAPI` libraries to escape any special HTML characters.

For example:

```jsp
<div>Hello, <%= org.apache.commons.text.StringEscapeUtils.escapeHtml4(request.getParameter("username")) %></div>
```

This would ensure that any special characters like `<`, `>`, and `&` in the `username` parameter are properly escaped and won't be interpreted as HTML or JavaScript by the browser.

### General best practices:
1. **Input Validation & Escaping**: Always escape user input when inserting it into HTML, JavaScript, CSS, or URLs.
2. **Use HTTP-only Cookies for Session Data**: To mitigate session hijacking, store sensitive data in cookies with the `HttpOnly` flag.
3. **Use Content Security Policy (CSP)**: Implementing CSP helps mitigate the impact of XSS by restricting what scripts are allowed to run on your website.


---
## Stored Xss :

**Example scenario for Stored XSS:**
Let's say your application allows users to submit their usernames, and the usernames are stored in a database. If an attacker can input something like this:


`<script>alert('XSS')</script>`
And the application retrieves and displays this stored value without properly sanitizing it, the script will execute whenever the stored data (the username) is displayed on a page.

**Example code (vulnerable):**
If the server saves the username in a database and later retrieves and displays it like this:

`<div>Hello, <%= request.getParameter("username") %></div>`
If username is stored with the malicious script, it will be **reflected back** to the user as part of the page when it is later viewed.

---
## DOM Xss:

**DOM-based XSS** (Document Object Model-based XSS) is a type of **client-side** Cross-Site Scripting vulnerability. Unlike **Stored** or **Reflected XSS**, where malicious payloads are executed when they are inserted into the response by the server, **DOM-based XSS** occurs entirely on the **client-side** (in the browser) when **malicious input is handled by JavaScript** in an insecure manner.

In DOM-based XSS, the vulnerability arises when **JavaScript** running in the browser takes **untrusted data** (e.g., from the URL, cookies, local storage, or form input) and **injects it into the DOM** without proper sanitization or escaping. This leads to execution of malicious scripts.

### Key Characteristics of DOM-based XSS:
- The malicious script is executed **entirely within the client-side environment** (in the user's browser).
- It typically involves **modifying the DOM** (using `document.getElementById()`, `document.write()`, `innerHTML`, etc.) using untrusted data.
- It is triggered by **JavaScript execution** rather than by the server's response.

### Example of DOM-based XSS:

Imagine a scenario where a web application uses URL query parameters to dynamically update content on the page. For instance:

```html
<!-- Vulnerable Example: -->
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>DOM XSS Example</title>
</head>
<body>
    <div id="output"></div>
    <script>
        // Get the 'name' parameter from the URL
        var name = new URLSearchParams(window.location.search).get('name');
        
        // Inject the 'name' parameter directly into the HTML without sanitization
        document.getElementById('output').innerHTML = 'Hello, ' + name;
    </script>
</body>
</html>
```

If an attacker submits a URL like this:

```
http://example.com/?name=<script>alert('XSS')</script>
```

The `name` parameter will be directly injected into the HTML without sanitization, causing the malicious JavaScript code (`<script>alert('XSS')</script>`) to be executed in the victim's browser, resulting in an **XSS attack**.

### How DOM-based XSS Happens:

1. The page loads, and JavaScript code accesses data from sources like the **URL**, **local storage**, **cookies**, or **user input**.
2. The untrusted data is used directly within the JavaScript code (e.g., with `innerHTML`, `document.write()`, or `eval()`).
3. The data is injected into the DOM or executed as JavaScript, which allows an attacker to inject their own code into the page.

### Common Vulnerable JavaScript Patterns:
1. **Using `innerHTML` or `outerHTML` without sanitization**:
   ```javascript
   document.getElementById('output').innerHTML = userInput; // Dangerous
   ```

2. **Using `document.write()` or `document.writeln()`**:
   ```javascript
   document.write(userInput); // Dangerous
   ```

3. **Using `eval()` or `setTimeout()`/`setInterval()` with user input**:
   ```javascript
   eval(userInput); // Dangerous (can execute arbitrary JavaScript)
   ```

4. **Using `window.location.hash` or `window.location.search` improperly**:
   ```javascript
   var param = window.location.hash.substring(1); // Fetching data from the URL
   document.getElementById('content').innerHTML = param; // Direct injection
   ```

### How to Prevent DOM-based XSS:

1. **Avoid Dangerous Methods like `innerHTML`, `document.write()`, and `eval()`**:
   Whenever possible, **avoid using these methods** with untrusted input. These are often sources of DOM-based XSS vulnerabilities because they allow the injection of raw HTML or JavaScript.

   Instead, use methods like:
   - `textContent` or `innerText` (to safely set text content)
   - `setAttribute()` (to safely set HTML attributes)

   **Good Example:**
   ```javascript
   // Use textContent instead of innerHTML to set plain text
   document.getElementById('output').textContent = userInput;
   ```

2. **Sanitize User Input**:
   Before using user input in the DOM, **sanitize** it to remove potentially dangerous content (like `<script>` tags, event handlers, etc.).

   You can use libraries like [DOMPurify](https://github.com/cure53/DOMPurify) to sanitize input before injecting it into the DOM.

   ```javascript
   var sanitizedInput = DOMPurify.sanitize(userInput);
   document.getElementById('output').innerHTML = sanitizedInput;
   ```

3. **Use `textContent` or `createTextNode`**:
   These methods are safe alternatives to `innerHTML` for injecting text into the DOM.

   ```javascript
   var textNode = document.createTextNode(userInput);
   document.getElementById('output').appendChild(textNode);
   ```

4. **Validate and Encode Input for JavaScript Context**:
   If you absolutely need to include user input in HTML attributes or JavaScript code, ensure you **escape** the data appropriately.

   For example, if you're adding user input to a URL, **encode** the input:

   ```javascript
   var userInput = encodeURIComponent(inputFromUser);
   ```

5. **CSP (Content Security Policy)**:
   Implement a **CSP** that helps block malicious scripts from running on your page. CSP can mitigate the impact of XSS, including DOM-based XSS, by restricting which scripts can run on your page.

6. **Use JavaScript Frameworks with Built-In XSS Protection**:
   Modern JavaScript frameworks like **React**, **Angular**, or **Vue.js** automatically escape data in templates to protect against XSS attacks. If you're building a JavaScript-heavy application, consider using such a framework to help reduce the risk of DOM-based XSS.

### Example of Secure Code:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Secure DOM XSS Example</title>
</head>
<body>
    <div id="output"></div>
    <script>
        // Secure approach: sanitize and escape input
        var name = new URLSearchParams(window.location.search).get('name');
        
        // Use textContent to avoid HTML injection
        document.getElementById('output').textContent = 'Hello, ' + name;
    </script>
</body>
</html>
```

### Conclusion:

**DOM-based XSS** is a client-side vulnerability that can occur when JavaScript uses unsanitized user input to update the DOM. This type of XSS requires developers to be cautious about how they handle and insert user data in the browser. By using safe methods for manipulating the DOM, sanitizing input, and avoiding risky JavaScript functions (like `innerHTML`, `eval()`, and `document.write()`), you can effectively protect your application from DOM-based XSS vulnerabilities.










