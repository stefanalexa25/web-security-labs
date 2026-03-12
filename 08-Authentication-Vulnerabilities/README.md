# Authentication Vulnerabilities

## What is it?
Authentication vulnerabilities arise when the mechanisms used to verify user identity are poorly implemented. Attackers can exploit these weaknesses to gain unauthorized access to accounts without knowing the valid credentials.

**Common types:**
- Username enumeration
- Brute force attacks
- Weak password policies
- Flawed "Remember me" functionality
- Insecure password reset flows
- Multi-factor authentication (MFA) bypass

---

## Examples

### Username Enumeration
Different error messages reveal whether a username exists:
```
"Invalid username"        → username does not exist
"Invalid password"        → username exists, wrong password
```
An attacker can use this to build a valid username list before brute forcing.

### Brute Force — No Rate Limiting
A login endpoint with no lockout or rate limiting can be attacked:
```
POST /login
username=admin&password=password1
username=admin&password=password2
username=admin&password=123456
...
```
Burp Suite Intruder can automate this with a wordlist.

### Insecure Password Reset
A reset token that is:
- Short or predictable (e.g. timestamp-based)
- Never expires
- Sent in a URL parameter that gets logged

...can be exploited to take over accounts.

---

## How to Prevent It
- **Use generic error messages** — never reveal whether username or password is wrong
- **Implement rate limiting and account lockout**
- **Enforce strong password policies**
- **Use secure, random, expiring tokens** for password resets
- **Implement MFA** for sensitive accounts
- **Log and monitor** failed authentication attempts

---

## Tools Used
- Burp Suite (Intruder for brute force testing, intercepting reset flows)

## References
- [PortSwigger: Authentication](https://portswigger.net/web-security/authentication)
- [OWASP: Authentication Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Authentication_Cheat_Sheet.html)
