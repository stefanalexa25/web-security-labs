# Server-Side Request Forgery (SSRF)

## What is it?
SSRF allows an attacker to make the server perform HTTP requests to arbitrary destinations — including internal services that are not accessible from the internet. This can expose internal infrastructure, cloud metadata endpoints, or other sensitive resources.

---

## Example
An application fetches a URL provided by the user:

```
POST /fetch
url=https://example.com/image.jpg
```

An attacker changes the URL to target an internal service:

```
url=http://192.168.1.1/admin
```

Or in cloud environments, to the metadata endpoint:

```
url=http://169.254.169.254/latest/meta-data/iam/security-credentials/
```

This can leak AWS IAM credentials, allowing full cloud account takeover.

---

## How to Prevent It
- **Allowlist** permitted domains and IP ranges
- **Block requests to internal IP ranges** (127.0.0.1, 169.254.x.x, 10.x.x.x, etc.)
- **Disable unnecessary URL fetch features**
- **Use a dedicated egress proxy** to control outbound requests
- **Validate and sanitize URLs** before processing

---

## Tools Used
- Burp Suite (intercepting and modifying requests, Collaborator for blind SSRF)

## References
- [PortSwigger: SSRF](https://portswigger.net/web-security/ssrf)
- [OWASP: SSRF](https://owasp.org/www-community/attacks/Server_Side_Request_Forgery)
