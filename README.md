# Web Application Security Labs

A practical documentation of web application security research conducted in controlled lab environments, focusing on **OWASP Top 10** vulnerabilities.

## Author
**Alexa Stefan-George**  
Computer Science Student @ Babeș-Bolyai University, Cluj-Napoca  
[LinkedIn](www.linkedin.com/in/stefangeorgealexa) | [GitHub]([#](https://github.com/stefanalexa25)

---

## About This Repository
This repository documents hands-on research into common web application vulnerabilities. For each vulnerability, I cover:
- What it is and how it works
- A practical example of exploitation
- How to prevent it

All research was conducted in **controlled lab environments** using **Burp Suite**.

---

## Vulnerabilities Covered

| # | Vulnerability | OWASP Category |
|---|--------------|----------------|
| 01 | [Cross-Site Scripting (XSS)](./01-XSS/) | A03: Injection |
| 02 | [SQL Injection (SQLi)](./02-SQLi/) | A03: Injection |
| 03 | [XML Injection & XXE](./03-XML-Injection-XXE/) | A05: Security Misconfiguration |
| 04 | [Cross-Site Request Forgery (CSRF)](./04-CSRF/) | A01: Broken Access Control |
| 05 | [Server-Side Template Injection (SSTI)](./05-SSTI/) | A03: Injection |
| 06 | [Server-Side Request Forgery (SSRF)](./06-SSRF/) | A10: SSRF |
| 07 | [OS Command Injection](./07-OS-Command-Injection/) | A03: Injection |
| 08 | [Authentication Vulnerabilities](./08-Authentication-Vulnerabilities/) | A07: Auth Failures |
| 09 | [Business Logic Flaws](./09-Business-Logic-Flaws/) | A04: Insecure Design |
| 10 | [File Upload Vulnerabilities](./10-File-Upload-Vulnerabilities/) | A05: Security Misconfiguration |

---

## Tools Used
- **Burp Suite** — intercepting and manipulating HTTP requests
- **Browser DevTools** — inspecting client-side behavior

## Resources
- [OWASP Top 10](https://owasp.org/www-project-top-ten/)
- [PortSwigger Web Security Academy](https://portswigger.net/web-security)
- [Pluralsight Web Security Labs](https://www.pluralsight.com)

---

> ⚠️ **Disclaimer:** All techniques documented here were practiced in controlled, legal lab environments. This repository is for educational purposes only.
