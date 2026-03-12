# Business Logic Flaws

## What is it?
Business logic flaws are vulnerabilities that arise from flawed assumptions in the design of an application's workflow. Unlike injection attacks, these don't exploit technical weaknesses — they abuse the intended functionality in unintended ways.

These are often the hardest vulnerabilities to detect with automated scanners because they require understanding of what the application is *supposed* to do.

---

## Examples

### Price Manipulation
An e-commerce application trusts the client-submitted price:
```
POST /checkout
item_id=123&price=0.01&quantity=1
```
If the server doesn't validate the price server-side, the attacker buys the item for 1 cent.

### Negative Quantity
```
POST /cart
item_id=123&quantity=-1
```
If not validated, this could reduce the total price or even generate store credit.

### Skipping Workflow Steps
A multi-step process (e.g. payment → confirmation → order placed) where the application doesn't enforce step order:
```
POST /order/confirm    ← attacker skips /order/pay entirely
```

### Privilege Escalation via Parameter Tampering
```
POST /update-profile
role=admin
```
If the server doesn't validate who can change roles, the attacker promotes themselves.

---

## How to Prevent It
- **Enforce business rules server-side** — never trust client-submitted data for pricing, quantities, or roles
- **Validate workflow sequence** — ensure steps cannot be skipped
- **Implement least privilege** — users should only access what they need
- **Thorough threat modeling** during design phase
- **Manual code review** — automated scanners often miss logic flaws

---

## Tools Used
- Burp Suite (intercepting and modifying requests to test workflow assumptions)

## References
- [PortSwigger: Business Logic Vulnerabilities](https://portswigger.net/web-security/logic-flaws)
- [OWASP: Business Logic Security](https://owasp.org/www-community/vulnerabilities/Business_logic_vulnerability)
