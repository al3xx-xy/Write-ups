# 🧾 PortSwigger Write-up: Blind OS command injection with time delays

## 🔍 Lab Info
- **Lab Name:** Blind OS command injection with time delays
- **Category:** Command injection
- **Level:** PRACTITIONER
- **Link:** [Here](https://portswigger.net/web-security/os-command-injection/lab-blind-time-delays)

---

## 🎯 Objective
**What is the goal of this lab?**  
To solve the lab, exploit the blind OS command injection vulnerability to cause a 10 second delay.

---

## 🧠 Key Concepts
- OS Command Injection
- Blind command injection

---

## 🛠️ Tools Used
- Firefox
- Burp Suite

---

## 🧪 Steps to Solve

### 1. Reconnaissance
- This lab contains a blind OS command injection vulnerability in the feedback function
- The application executes a shell command containing the user-supplied details. The output from the command is not returned in the response.
### 2. Testing for Vulnerability
- modify field by field and see which one take 10 second delay using `& sleep 10 #`
- result the email field is vulnerable


### 3. Final Payload
**Payload:**  
```bash
&email=alex@gmail.com & sleep 10 # => &email=alex@gmail.com%26sleep%2010#
```


---

## ✅ Conclusion

**What did you learn from this lab?**
- Blind command injection does not return output in the response.
- Time delays like `sleep 10` can be used to detect if the command was executed.
- It’s important to test each input field individually.
