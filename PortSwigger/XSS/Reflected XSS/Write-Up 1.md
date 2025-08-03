#reflected-xss

Reflected XSS into HTML context with nothing encoded : [Link](https://portswigger.net/web-security/cross-site-scripting/reflected/lab-html-context-nothing-encoded)

This lab contains a simple reflected cross-site scripting vulnerability in the *search* functionality.

As we can see, when I attempt to search for something, like in this example *XSS*, the application directly writes it to the page.

<img src="IMG/S1.png">

And in the page's source code, as we can see, it is added inside the `<h1>` tag.

<img src="IMG/S2.png">

When I type `<script>alert('XSS')</script>` into the search field, the input is reflected in the page's HTML and executed.

<img src="IMG/S3.png">
