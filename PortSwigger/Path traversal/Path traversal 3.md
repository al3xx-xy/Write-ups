> Mon 4 Aug 2025
> al3xx

# 🧾 PortSwigger Write-up: File path traversal, traversal sequences stripped non-recursively

## 🔍 Lab Info
- **Lab Name:** File path traversal, traversal sequences stripped non-recursively
- **Category:** Path traversal
- **Level:** PRACTITIONER
- **Link:** [Here](https://portswigger.net/web-security/file-path-traversal/lab-sequences-stripped-non-recursively)

---

## 🎯 Objective
**What is the goal of this lab?**  
*To solve the lab, retrieve the contents of the `/etc/passwd` file*

---

## 🧠 Key Concepts
- Path traversal
- Traversal sequences stripped non-recursively

---

## 🛠️ Tools Used
- Firefox
- Burp Suite

---

## 🧪 Steps to Solve

### 1. Reconnaissance
- The application lets users view images using a `filename` parameter.
- Attempts to use `../` for directory traversal are **blocked** or **filtred**.

### 2. Testing for Vulnerability 
- Tried submitting: `../../../../../etc/passwd` and it blocked
- Tried submitting : `../\etc/\passwd` and it blocked

### 3. Bypassing Filters (if needed)
- Instead of using normal traversal sequences like `../`, try duplicating them by submitting: `....//....//....//....//etc//passwd`
- - The server **does not block duplicate paths**, and the file gets read.

### 4. Final Payload
**Payload:**  
```TEXT
/image?filename=....//....//....//....//etc//passwd
```

---

## ✅ Conclusion

**What did you learn from this lab?**
-  Blocking `../` sequences is not always enough to stop path traversal.
-  Duplicate path like `....//....//etc//passwd` can bypass weak filters.