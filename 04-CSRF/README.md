# Cross-Site Request Forgery (CSRF)

## What is it?
CSRF tricks an authenticated user into unknowingly submitting a malicious request to a web application they are logged into. Since the browser automatically includes session cookies, the server processes the request as if it were legitimate.

---

## Example
A user is logged into their bank. An attacker sends them a malicious page containing:

```html
<form action="https://bank.com/transfer" method="POST">
  <input type="hidden" name="to" value="attacker_account" />
  <input type="hidden" name="amount" value="5000" />
</form>
<script>document.forms[0].submit();</script>
```

When the victim visits the page, the form auto-submits using their active session — transferring money without their knowledge.

---

## How to Prevent It
- **CSRF Tokens** — include a unique, unpredictable token in every state-changing request
- **SameSite Cookie attribute** — set to `Strict` or `Lax` to prevent cross-site cookie sending
- **Check Origin/Referer headers** — validate that requests originate from your domain
- **Re-authentication** — require password confirmation for sensitive actions

---

## Tools Used
- Burp Suite (intercepting requests, generating CSRF PoC)

## References
- [PortSwigger: CSRF](https://portswigger.net/web-security/csrf)
- [OWASP: CSRF](https://owasp.org/www-community/attacks/csrf)
