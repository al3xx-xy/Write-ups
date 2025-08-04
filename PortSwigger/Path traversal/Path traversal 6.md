> Mon 4 Aug 2025
> al3xx

# 🧾 PortSwigger Write-up: File path traversal, validation of file extension with null byte bypass

## 🔍 Lab Info
- **Lab Name:** File path traversal, validation of file extension with null byte bypass
- **Category:** Path traversal
- **Level:** PRACTITIONER
- **Link:** [Here](https://portswigger.net/web-security/file-path-traversal/lab-validate-file-extension-null-byte-bypass)

---

## 🎯 Objective
**What is the goal of this lab?**  
*To solve the lab, retrieve the contents of the `/etc/passwd` file.*

---

## 🧠 Key Concepts
- Path traversal
- validation of file extension with null byte bypass

---

## 🛠️ Tools Used
- Firefox
- Burp Suite

---

## 🧪 Steps to Solve

### 1. Reconnaissance
Blocks all paths that does not end with *.jpg*

### 2. Testing for Vulnerability
- Tried injecting: `../../../../etc/passwd.jpg`
- The server responded that the file does not exist

### 3. Bypassing Filters (if needed)
- Tried injecting: `filename=../../../etc/passwd%00.jpg`
- The server accepted the request and returned the contents

### 4. Final Payload
**Payload:**  
```TEXT
filename=../../../etc/passwd%00.jpg
```

---

## ✅ Conclusion

**What did you learn from this lab?**
- File extension validation alone is not sufficient to prevent path traversal.
- Using a null byte (`%00`) can trick the server into treating the filename as ending earlier than it appears, effectively bypassing extension checks.
