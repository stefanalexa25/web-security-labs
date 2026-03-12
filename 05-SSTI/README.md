# Server-Side Template Injection (SSTI)

## What is it?
SSTI occurs when user input is embedded directly into a server-side template without sanitization. Template engines (like Jinja2, Twig, Freemarker) are designed to execute code — if an attacker can inject template syntax, they can execute arbitrary code on the server.

---

## Example
An application uses Jinja2 and renders user input directly:

```python
template = "Hello " + request.args.get('name')
return render_template_string(template)
```

An attacker inputs:
```
{{7*7}}
```

If the response shows `49`, the template is being evaluated — confirming SSTI.

**Escalating to Remote Code Execution (RCE):**
```
{{config.__class__.__init__.__globals__['os'].popen('id').read()}}
```

This executes the `id` command on the server.

---

## How to Prevent It
- **Never pass user input directly into templates** — treat it as data, not code
- **Use sandboxed template environments** where available
- **Validate and sanitize input** strictly
- **Use logic-less templates** (e.g. Mustache) where possible

---

## Tools Used
- Burp Suite (intercepting and modifying requests)

## References
- [PortSwigger: SSTI](https://portswigger.net/web-security/server-side-template-injection)
- [OWASP: SSTI](https://owasp.org/www-project-web-security-testing-guide/v41/4-Web_Application_Security_Testing/07-Input_Validation_Testing/18-Testing_for_Server_Side_Template_Injection)
