## Cross-Site Scripting (XSS)
* Stored XSS: Malicious scripts are injected and stored on the server (e.g., in databases), and are executed in the user’s browser when they visit the affected page.
* Reflected XSS: The malicious script is reflected off a web server and executed in the user's browser immediately.
* DOM-based XSS: The vulnerability exists in the client-side script, where malicious scripts can manipulate the Document Object Model (DOM).

Here’s the information about XSS formatted for GitHub Markdown:

```markdown
# Cross-Site Scripting (XSS)

Cross-Site Scripting (XSS) is a type of web security vulnerability that allows attackers to inject malicious scripts into webpages viewed by other users. These scripts can steal sensitive data, such as cookies, session tokens, or even take control of the user's browser.

## Types of XSS

XSS can be classified into three main types:

### 1. Stored (Persistent) XSS
- **What it is**: The malicious script is stored on the server (e.g., in a database) and displayed to users when they view the affected page.
- **Example**: A user submits a comment on a blog, and the comment contains a script. The script is stored in the database and runs whenever another user views the comment.
- **Impact**: High, because the script will run for any user who visits the affected page.
- **Example Attack**:
  ```html
  <script>alert('XSS Attack!');</script>
  ```
  Whenever someone views the page with the comment, the script executes, potentially stealing session data.

### 2. Reflected (Non-Persistent) XSS
- **What it is**: The malicious script is part of the URL or form input, and it gets reflected back in the response, directly executing in the user's browser.
- **Example**: A user clicks a malicious link crafted by the attacker, which includes a script in the URL. The server reflects the input back in its response, and the script executes in the victim's browser.
- **Impact**: Medium, as it requires user interaction (e.g., clicking a link).
- **Example Attack**:
  An attacker sends a link like:
  ```
  http://example.com/search?q=<script>alert('XSS!');</script>
  ```
  If the website doesn't sanitize user input, this script will run in the user's browser when they click the link.

### 3. DOM-based XSS
- **What it is**: The malicious script is executed in the client-side (browser) environment, and the vulnerability exists in the JavaScript code running on the page, not on the server.
- **Example**: A web page uses JavaScript to take a value from the URL and insert it into the page. If that value is not sanitized, an attacker can inject a script into the URL that gets executed in the user's browser.
- **Impact**: Medium to High, depending on how the script is executed and what actions it can perform.
- **Example Attack**:
  A page might take a value from the URL, like `example.com?name=Jayesh`, and display it:
  ```javascript
  document.write("Welcome, " + location.search.substring(1));
  ```
  An attacker could change the URL to:
  ```
  http://example.com?name=<script>alert('XSS!');</script>
  ```

## How XSS Works
XSS exploits occur when:
1. A web application takes untrusted input from a user (e.g., a form, URL parameter) and includes it in the output HTML without proper validation or escaping.
2. The browser interprets the malicious script as legitimate code and executes it in the context of the vulnerable site.

## Consequences of XSS
- **Stealing cookies and session tokens**: Attackers can use XSS to steal session cookies and impersonate the victim.
- **Keylogging**: Injecting a keylogger to capture everything the user types.
- **Phishing attacks**: Displaying fake login forms to steal credentials.
- **Defacement**: Modifying the webpage content to mislead or scare users.
- **Browser control**: Running commands in the victim’s browser on behalf of the attacker.

## Example Scenario
Consider an online shopping site with a search box that reflects user input in the search results without any sanitization:
```html
Search results for "<b>search term</b>"
```
If the attacker enters:
```html
<script>alert('XSS')</script>
```
The page might render:
```html
Search results for "<script>alert('XSS')</script>"
```
And the script will execute an alert box. This could be escalated to steal cookies or session data.

## Prevention of XSS
1. **Input validation**: Always validate and sanitize user input to ensure that it doesn’t contain potentially harmful code.
2. **Output encoding**: Escape user input before displaying it in the browser, converting special characters (`<`, `>`, `"`, `'`) into safe versions (`&lt;`, `&gt;`, etc.).
3. **Use security libraries**: Use libraries like **OWASP ESAPI** or frameworks with built-in security features that help prevent XSS.
4. **Content Security Policy (CSP)**: Implement CSP headers to restrict the execution of inline scripts or untrusted sources.
5. **HTTP-only cookies**: Set cookies as HTTP-only so that they are not accessible via JavaScript.

## Example of Proper Output Encoding
Before displaying user input, convert potentially dangerous characters into their safe equivalents. For example:
```html
<script>alert('XSS')</script>
```
Would become:
```html
&lt;script&gt;alert('XSS')&lt;/script&gt;
```
This would prevent the browser from treating it as executable code.

By understanding these types of XSS and how to prevent them, you can protect web applications from these dangerous attacks.
```

You can copy and paste this formatted text directly into your GitHub README or any Markdown-supported platform! Let me know if you need any further adjustments!
