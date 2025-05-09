
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

### 5. Header Injection
- JWT Header Injection uses **custom JWK headers** to **bypass verification**.

#### Steps:
1. Install Burp Extensions: `JWT Editor`, `JSON Web Token`
2. Generate a **new RSA key** in the extension
3. Go to the request in Repeater ➡️ JWT Editor ➡️ `Attack` ➡️ `Embedded JWK`
4. Select your custom RSA key ➡️ Send the request

---

### 6. KID Injection
- The `kid` parameter can be exploited by pointing to **file directories**.

#### Steps:
1. In JWT Editor Keys ➡️ Create a **New Symmetric Key**
2. Change the `k` value to base64-encoded null byte: `AA==`
3. In Repeater ➡️ JWT Editor ➡️ Modify `kid` to:  
   ```
   ../../../../../dev/null
   ```
4. Sign the JWT using the same symmetric key.

---

### 7. Algorithm Confusion in JWT
- Happens when you get access to the **JWK token** from `/jwks.json`.

#### Steps:
1. Get the JWK key from `/jwks.json`
2. In Burp JWT Editor ➡️ `New RSA Key` ➡️ Use `JWK` format
3. Copy Public Key as PEM ➡️ Encode it in Base64
4. Create a **New Symmetric Key**, replace the `k` value with Base64
5. Modify JWT values and **sign using the symmetric key**

---

## 🧪 Bug Bounty Tip

- Always **create two user accounts**.
- Compare JWT tokens and try accessing other user sessions by tweaking the token.
