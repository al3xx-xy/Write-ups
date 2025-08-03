# 🧾 PortSwigger Write-up: OS command injection, simple case

## 🔍 Lab Info
- **Lab Name:** OS command injection, simple case
- **Category:** Command injection
- **Level:** APPRENTICE
- **Link:** [Here](https://portswigger.net/web-security/os-command-injection/lab-simple)

---

## 🎯 Objective
**What is the goal of this lab?**  
To solve the lab, execute the `whoami` command to determine the name of the current user.

---

## 🧠 Key Concepts
- OS Command Injection

---

## 🛠️ Tools Used
- Firefox
- Burp Suite

---

## 🧪 Steps to Solve

### 1. Reconnaissance
- The lab has a form to check whether a product is in stock.
- The input is a tracking number (e.g., `?productId=1&storeId=1`).
- Submit a request and intercept it using Burp.

### 2. Testing for Vulnerability
- Modify the `storeId` parameter with this payload `&storeId=1 & echo Hello`
- result = `54 Hello`

### 3. Final Payload
**Payload:**  
```bash
productId=1&storeId=1+%26+whoami
```

---

## ✅ Conclusion

**What did you learn from this lab?**
* Basic command injection occurs when user input is concatenated into OS commands.