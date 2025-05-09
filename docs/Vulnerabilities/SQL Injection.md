
# SQL Injection Cheat Sheet

SQL Injection is a vulnerability that allows attackers to interfere with the queries an application makes to its database. This document outlines different techniques and tools for exploiting SQL Injection vulnerabilities.

---

## 🧪 Manual & Automated Testing

- Basic SQLi testing starts with either manual payloads or automated tools like **SQLmap**.
- Manual techniques include:
  - `UNION` based attacks
  - `ORDER BY` clause testing
  - Error-based enumeration

### 🔧 SQLmap Flags:
- `--dbs` : Enumerate databases
- `-D [DATABASE NAME] --tables` : List tables in a specific database
- `-D [DATABASE] -T [TABLE] --dump` : Dump columns and data from a specific table

---

## 🕶️ Blind SQL Injection

Blind SQLi occurs when the application does not display database errors but still reacts differently based on the query's logic.

### 🔡 SUBSTRING Based Attacks

- Brute force character by character:
  ```sql
  SELECT substring(database(),1,1)
  SELECT if(substring(database(),1,1)='a',SLEEP(3),'a')
  SELECT if(substring(database(),1,1)>'g',SLEEP(3),'a')
  ```

### 🧮 Boolean Based SQLi

- Test logic:
  ```sql
  ' AND 1=1 -- -
  ' AND 1=2 -- -
  ```

### ⏱️ Time Based SQLi

- Time delay if condition is true:
  ```sql
  SELECT SLEEP(10)
  ```

### 💥 Error Based SQLi

- Example using `CASE` statement:
  ![image.png](../../assets/image_1737020823461_0.png)

- Conditionally returns 'a' if false:
  ```sql
  SELECT CASE WHEN (condition) THEN '' ELSE 'a' END
  ```

- Further reference: [DB Fiddle Example](https://www.db-fiddle.com/f/nLpyQDMd49iRygnY9H7CB8/5)

---

## 🕵️ Blind SQLi in Cookies / Sessions

- Blind SQLi isn't limited to URL parameters.
- It can be hidden in:
  - **Session Tokens**
  - **Cookies**

### Example:
```http
TrackingId=xyz'; SELECT SLEEP(10) --
```

Explore real-world labs at **PortSwigger Web Security Academy** for hands-on experience.

---

## 🧬 NoSQL Injection

- A unique form of injection targeting NoSQL databases like **MongoDB**.
- Most common injection points:
  - `username`
  - `password`

### Tips:
- Consult the [MongoDB Docs](https://www.mongodb.com/)
- Logical flaws in queries are often exploited with JSON-based payloads.

---

> ⚠️ Only test on systems you have **explicit permission** to test.

---

**© 2025 Daksh Bhagwani | DBugs.org**
