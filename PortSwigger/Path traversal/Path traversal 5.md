> Mon 4 Aug 2025
> al3xx

# 🧾 PortSwigger Write-up: File path traversal, validation of start of path

## 🔍 Lab Info
- **Lab Name:** File path traversal, validation of start of path
- **Category:** Path traversal
- **Level:** PRACTITIONER
- **Link:** [Here](https://portswigger.net/web-security/file-path-traversal/lab-validate-start-of-path)

---

## 🎯 Objective
**What is the goal of this lab?**  
*To solve the lab, retrieve the contents of the `/etc/passwd` file.*

---

## 🧠 Key Concepts
- validation of start of path

---

## 🛠️ Tools Used
- Firefox
- Burp Suite

---

## 🧪 Steps to Solve

### 1. Reconnaissance
- Blocks all path that does not start with `/var/www/images/`

### 2. Testing for Vulnerability
- Tried to use `filename=/var/www/images/../../../etc/password` 
- The server does not block paths that start with */var/www/images/*

### 4. Final Payload
**Payload:**  
```TEXT
filename=/var/www/images/../../../etc/password
```

---
### 
## ✅ Conclusion

**What did you learn from this lab?**
- Validating that the path starts with a specific base directory (e.g., `/var/www/images/`) is not enough to prevent path traversal.
- If the application doesn't normalize the path before validation, attackers can bypass restrictions using sequences like `../../../` to access sensitive files.