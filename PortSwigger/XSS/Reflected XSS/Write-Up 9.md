#reflected-xss 

Reflected XSS into a JavaScript string with angle brackets and double quotes HTML-encoded and single quotes escaped [link](https://portswigger.net/web-security/cross-site-scripting/contexts/lab-javascript-string-angle-brackets-double-quotes-encoded-single-quotes-escaped)

This lab contains a reflected cross-site scripting vulnerability in the search query tracking functionality where angle brackets and double are HTML encoded and single quotes are escaped

This challenge is similar to the previous one, but with one main difference:  
In this challenge, the single quote (`'`) is **escaped using a backslash** (`\`), which means we need to bypass it correctly.
`\';alert(1);//' 