> Mon 3 Aug 2025
> al3xx

# 🧾 PortSwigger Write-up: Blind OS command injection with output redirection

## 🔍 Lab Info
- **Lab Name:** Blind OS command injection with output redirection
- **Category:** Command injection
- **Level:** PRACTITIONER
- **Link:** [Here](https://portswigger.net/web-security/os-command-injection#how-to-prevent-os-command-injection-attacks)

---

## 🎯 Objective
**What is the goal of this lab?**  
To solve the lab, execute the `whoami` command and retrieve the output.

---

## 🧠 Key Concepts
- OS Command Injection
- Blind command injection
- Output redirection

---

## 🛠️ Tools Used
- Firefox
- Burp Suite
---

## 🧪 Steps to Solve

### 1. Reconnaissance
- This lab contains a blind OS command injection vulnerability in the feedback function.
- The application executes a shell command containing the user-supplied details. The output from the command is not returned in the response. However, you can use output redirection to capture the output from the command. There is a writable folder at: `/var/www/images/`
- The application serves the images for the product catalog from this location. You can redirect the output from the injected command to a file in this folder, and then use the image loading URL to retrieve the contents of the file.

### 2. Testing for Vulnerability
- Modify field by field to see which one will cause the delay.
- Result: email field is vulnerable
- Now is time to use this vulnerability to redirect output
- before redirect output we should check where is the endpoit to get images in the website 
- result `/image?filename=`
- now time to inject command and save the value in `/var/www/images` and read it from the endpoint


### 3. Final Payload
**Payload 1:**  
```html
&email=c%40gmail.com+%26+sleep+10+%23
```

**Payload 2:**
```bash
&email=alex%40gmail.com+%26+whoami+>+/var/www/images/whoami.txt+%26
```

---

## ✅ Conclusion

**What did you learn from this lab?**
- Blind OS command injection doesn't return output directly, but can be exploited using time delays or output redirection.
- Redirecting output to a web-accessible directory allows attackers to read command results.