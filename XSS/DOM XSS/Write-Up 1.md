#DOM-XSS

DOM XSS in `document.write` sink using source `location.search`:  [link](https://portswigger.net/web-security/cross-site-scripting/dom-based/lab-document-write-sink)

This lab contains a DOM-based cross-site scripting vulnerability in the search query tracking functionality. It uses the JavaScript `document.write` function, which writes data out to the page. The `document.write` function is called with data from `location.search`, which you can control using the website URL.

in this challenge it contain a basic DOM-XSS that it take the search value and injected into the Document 

<img src="IMG/S1.png">
like we can see in the images above the value of `(window.location.search)` goes to `query` variable and the query goes into `trackSearch` function so the solve on this challenge is broke the `query` variable we can do this using this payload :
`XSSPOC"> <img src=x onerror=alert(1)>//`
