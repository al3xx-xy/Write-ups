# 🧾 PortSwigger Write-up: File path traversal, simple case

## 🔍 Lab Info
- **Lab Name:** File path traversal, simple case
- **Category:** Path traversal
- **Level:** APPRENTICE
- **Link:** [Here](https://portswigger.net/web-security/file-path-traversal/lab-simple)

---

## 🎯 Objective
**What is the goal of this lab?**  
To solve the lab, retrieve the contents of the `/etc/passwd` file.

---

## 🧠 Key Concepts
- File Path Traversal
- Reading sensitive files using directory traversal

---

## 🛠️ Tools Used
- Firefox
- Burp Suite

---

## 🧪 Steps to Solve

### 1. Reconnaissance
- The application serves product images using a `filename` parameter in the URL.
- Example:  `/image?filename=picture.jpg`
- - Try changing the `filename` parameter to access files outside the images directory.

### 2. Testing for Vulnerability
- Tried accessing files like: `/image?filename=../../../etc/passwd`
- After a few attempts, confirmed that the application allows traversal using `../`.

### 3. Final Payload
**Payload:**  
```html
/image?filename=../../../etc/passwd
```

---

## ✅ Conclusion

**What did you learn from this lab?**
- File path traversal vulnerabilities allow attackers to access files outside the intended directory.
- Using `../` lets you move up in the directory structure.
- Always sanitize and validate file path inputs.