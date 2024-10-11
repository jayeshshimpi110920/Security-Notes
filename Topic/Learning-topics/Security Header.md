
## Security Header
---
| **Security Header**               | **Description**                                               | **Prevention/Mitigation**                          | **Parameter Values**                                | Keep it |
|------------------------------------|-------------------------------------------------------------|---------------------------------------------------|----------------------------------------------------|---|
| **Content Security Policy (CSP)**  | Controls sources of content for pages.                     | Prevents XSS and data injection attacks.          | `default-src`, `script-src`, `img-src`, etc.      |
| **X-Frame-Options**                | Restricts how pages can be framed.                          | Mitigates clickjacking.                           | `DENY`, `SAMEORIGIN`, `ALLOW-FROM uri`             |
| **Strict-Transport-Security (HSTS)**| Enforces secure (HTTPS) connections.                       | Prevents man-in-the-middle attacks.               | `max-age`, `includeSubDomains`, `preload`          |
| **X-Content-Type-Options**         | Prevents browsers from MIME type sniffing.                  | Mitigates MIME type confusion attacks.            | `nosniff`                                          | `nosniff`
| **Referrer-Policy**                | Controls referrer information sent to other sites.          | Protects user privacy.                            | `no-referrer`, `no-referrer-when-downgrade`, etc. |
| **X-XSS-Protection**               | Enables XSS filtering in browsers.                          | Prevents reflected XSS attacks.                   | `0` (disabled), `1` (enabled)                      | 1 `mode=blocked`|
| **Feature-Policy**                 | Controls which features can be used in the browser.        | Limits potential attack vectors.                  | Various directives like `geolocation`, `camera`    |
| **Permissions-Policy**             | Replaces Feature-Policy to control features and APIs.      | Similar to Feature-Policy.                        | Various directives like `geolocation`, `camera`    |
| **Cache-Control**                  | Directs caching mechanisms in browsers.                     | Prevents caching of sensitive data.               | `no-store`, `no-cache`, `must-revalidate`          |
| **Content-Disposition**             | Suggests how content should be handled.                     | Prevents content types from being downloaded incorrectly. | `attachment`, `inline`                          |

Implementing these security headers is crucial for protecting web applications from various security threats.
