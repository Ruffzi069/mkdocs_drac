
# JWT Vulnerabilities & Techniques

## 🔐 About HS256
- **HS256** is an old and rarely used symmetric encryption algorithm.
- Being **symmetric**, it uses the **same key** to both encrypt and decrypt.
- If HS256 is found in use, **you may try cracking it**.
- Sometimes, JWT tokens seen in requests are **false positives** — they don't actually control access.

---

## 🔍 JWT Testing Techniques

### 1. Modifying the Payload
- You can **modify the JWT payload** to escalate privileges.
- Example: Change `user:guest` ➡️ `user:admin`
```json
{
  "id": 34234214,
  "user": "admin"
}
```

---

### 2. Changing the Signature Algorithm
- Alter the JWT algorithm from `RS256` to `HS256`, `HS512`, etc.
- This can help **bypass validations** on vulnerable systems.

---

### 3. Removing the Signature
- Set the algorithm to `none` and **remove the signature** completely.
- This results in a token like:
```
Header.Payload.
```

---

### 4. Brute Forcing Weak Signature Keys
- Use the [`ticarpi/jwt_tool`](https://github.com/ticarpi/jwt_tool) to brute-force weak keys:
```bash
python3 jwt_tool.py [JWT_TOKEN] --crack -d [WORDLIST]
```
- Refer to online attack books for further fuzzing techniques.

---

## 🧪 Bug Bounty Tip

- Always **create two user accounts**.
- Compare JWT tokens and try accessing other user sessions by tweaking the token.
