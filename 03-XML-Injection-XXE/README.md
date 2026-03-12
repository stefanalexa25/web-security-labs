# XML Injection & XML External Entity (XXE)

## What is it?
**XML Injection** occurs when user input is embedded in XML without sanitization, allowing attackers to manipulate the XML structure.

**XXE (XML External Entity)** is a more severe variant where an attacker abuses the XML parser's support for external entities to read local files, perform SSRF, or execute denial-of-service attacks.

---

## Example

### XXE — Reading Local Files
An application parses XML input:

```xml
<?xml version="1.0"?>
<!DOCTYPE foo [
  <!ENTITY xxe SYSTEM "file:///etc/passwd">
]>
<user><name>&xxe;</name></user>
```

If the XML parser processes external entities, it returns the contents of `/etc/passwd` in the response.

### XXE — SSRF via XXE
```xml
<!DOCTYPE foo [
  <!ENTITY xxe SYSTEM "http://internal-server/admin">
]>
```

---

## How to Prevent It
- **Disable external entity processing** in the XML parser (most important)
- **Use JSON instead of XML** where possible
- **Validate and sanitize** XML input
- **Patch XML libraries** — many older parsers enable external entities by default
- **Use allowlists** for expected XML structure

---

## Tools Used
- Burp Suite (intercepting and modifying XML requests)

## References
- [PortSwigger: XXE](https://portswigger.net/web-security/xxe)
- [OWASP: XXE](https://owasp.org/www-community/vulnerabilities/XML_External_Entity_(XXE)_Processing)
