# OS Command Injection

## What is it?
OS Command Injection occurs when an application passes user-supplied data to a system shell without proper sanitization. An attacker can append additional commands, gaining the ability to execute arbitrary OS commands on the server with the application's privileges.

---

## Example
An application pings a host provided by the user:

```python
os.system("ping -c 1 " + user_input)
```

An attacker inputs:
```
127.0.0.1; cat /etc/passwd
```

The shell executes:
```bash
ping -c 1 127.0.0.1; cat /etc/passwd
```

Both commands run — the second revealing the server's passwd file.

**Common shell operators used:**
| Operator | Behavior |
|----------|----------|
| `;` | Run second command regardless |
| `&&` | Run second command only if first succeeds |
| `\|\|` | Run second command only if first fails |
| `\|` | Pipe output of first into second |
| `` `cmd` `` | Inline command execution |

---

## How to Prevent It
- **Avoid system shell calls** — use language-native libraries instead (e.g. Python's `subprocess` with argument lists, not shell=True)
- **Whitelist allowed input values** strictly
- **Escape shell metacharacters** if shell calls are unavoidable
- **Run applications with least privilege** to limit damage

---

## Tools Used
- Burp Suite (intercepting and modifying requests)

## References
- [PortSwigger: OS Command Injection](https://portswigger.net/web-security/os-command-injection)
- [OWASP: Command Injection](https://owasp.org/www-community/attacks/Command_Injection)
