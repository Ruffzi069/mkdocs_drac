## 🛡️ CSRF (Cross-Site Request Forgery)

### 📖 Definition
CSRF exploits the trust a web app has in the user's browser, making **unauthorized actions** on behalf of an authenticated user.

### ⚠️ Example Attack
```html
<form action="https://bank.com/transfer" method="POST">
  <input type="hidden" name="to" value="attacker">
  <input type="hidden" name="amount" value="1000">
</form>
<script>document.forms[0].submit();</script>
```

### ✅ Mitigations
- Use **CSRF tokens** in forms.
- Set **SameSite** cookies.
- Use **double submit cookie** strategy.
- Require **user interaction or re-authentication** for sensitive actions.

### 🔧 Testing Tools:

- **Burp Suite** – Intercept and manipulate CSRF-prone requests.
  > Use **"Generate CSRF PoC"** feature in Burp's Repeater/Proxy.

- **Postman** – Test endpoints with and without CSRF tokens.
  ```http
  POST /update_email HTTP/1.1
  Host: example.com
  Content-Type: application/x-www-form-urlencoded
  Cookie: sessionid=12345

  email=attacker@example.com
  ```

---

