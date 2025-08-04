> Mon 4 Aug 2025
> al3xx

# 🧾 PortSwigger Write-up: File path traversal, traversal sequences stripped with superfluous URL-decode

## 🔍 Lab Info
- **Lab Name:** File path traversal, traversal sequences stripped with superfluous URL-decode
- **Category:** Path traversal
- **Level:** PRACTITIONER
- **Link:** [Here](https://portswigger.net/web-security/file-path-traversal/lab-superfluous-url-decode)

---

## 🎯 Objective
**What is the goal of this lab?**  
*To solve the lab, retrieve the contents of the `/etc/passwd` file.*

---

## 🧠 Key Concepts
- Path traversal
- traversal sequences stripped with superfluous URL-decode

---

## 🛠️ Tools Used
- Firefox
- Burp Suite

---

## 🧪 Steps to Solve

### 1. Reconnaissance
- The application lets users view images using a `filename` parameter.
- Attempts to use `../../../../etc/passwd` for directory traversal are **blocked**.

### 2. Testing for Vulnerability
- Tried to use `....//....//....//....//etc//passwd` and it also blocked.
- Tried url encode `..%2F..%2F..%2F..%2F..%2Fetc%2Fpasswd` and it also blocked.


### 3. Bypassing Filters (if needed)
- Instead of using normal traversal sequences like `../` or url encode for it , try do double url encode   by submitting: `..%252F..%252F..%252Fetc%252Fpasswd`
- The server **does not block duplicate paths**, and the file gets read.

### 4. Final Payload
**Payload:**  
```TEXT
..%252F..%252F..%252F..%252F..%252Fetc%252Fpasswd
```

---

## ✅ Conclusion

**What did you learn from this lab?**
-  Blocking `../` sequences is not always enough to stop path traversal.
-  Blocking `....//....//etc//passwd` sequences is not always enough to stop path traversal.
- Double url encode  `..%252..%252FFetc%252FFpasswd` can bypass weak filters.