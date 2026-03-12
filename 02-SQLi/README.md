# SQL Injection (SQLi)

## What is it?
SQL Injection occurs when user-supplied input is inserted directly into a SQL query without proper sanitization. An attacker can manipulate the query to read, modify, or delete database data, bypass authentication, or in some cases execute OS commands.

---

## Example
A login form builds a query like this:

```sql
SELECT * FROM users WHERE username = 'admin' AND password = 'password123';
```

An attacker enters `' OR '1'='1` as the username:

```sql
SELECT * FROM users WHERE username = '' OR '1'='1' AND password = '';
```

Since `'1'='1'` is always true, the attacker logs in without valid credentials.

**Extracting data with UNION:**
```sql
' UNION SELECT username, password FROM users--
```

---

## How to Prevent It
- **Parameterized queries / Prepared Statements** — the most effective defense
- **Stored Procedures** — with proper parameterization
- **Input validation** — whitelist expected input formats
- **Least privilege** — database accounts should have minimal permissions
- **WAF (Web Application Firewall)** — as an additional layer

---

## Tools Used
- Burp Suite (intercepting requests, manual injection testing)

## References
- [PortSwigger: SQL Injection](https://portswigger.net/web-security/sql-injection)
- [OWASP: SQL Injection](https://owasp.org/www-community/attacks/SQL_Injection)
