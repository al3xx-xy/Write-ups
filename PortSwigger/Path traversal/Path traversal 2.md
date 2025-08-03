# 🧾 PortSwigger Write-up: File path traversal, traversal sequences blocked with absolute path bypass

## 🔍 Lab Info
- **Lab Name:** File path traversal, traversal sequences blocked with absolute path bypass
- **Category:** Path traversal
- **Level:** PRACTITIONER
- **Link:** [Here](https://portswigger.net/web-security/file-path-traversal/lab-absolute-path-bypass)

---

## 🎯 Objective
**What is the goal of this lab?**  
To solve the lab, retrieve the contents of the `/etc/passwd` file.

---

## 🧠 Key Concepts
- Path traversal
- traversal sequences blocked
---

## 🛠️ Tools Used
- Firefox
- Burp Suite

---

## 🧪 Steps to Solve

### 1. Reconnaissance
- The application lets users view images using a `filename` parameter.
- Attempts to use `../` for directory traversal are **blocked**.
- The application treats the filename as relative to a working directory (e.g., `/var/www/images`).

### 2. Testing for Vulnerability
- Tried submitting: `?filename=../../../etc/passwd`
- Request is **blocked** due to traversal filter.

### 3. Bypassing Filters
- Instead of using traversal (`../`), we try supplying an **absolute path** directly: `/etc/passwd`
- The server **does not block absolute paths**, and the file gets read.
### 4. Final Payload
**Payload:**  
```html
?filename=/etc/passwd
```

---

## ✅ Conclusion

**What did you learn from this lab?**
- Blocking `../` sequences is not always enough to stop path traversal.
- Absolute paths like `/etc/passwd` can bypass weak filters.
- Proper validation should enforce **whitelisting allowed paths**, not just blocking patterns.
