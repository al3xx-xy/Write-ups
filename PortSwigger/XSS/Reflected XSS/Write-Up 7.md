#reflected-xss

Reflected XSS in canonical link tag: [link](https://portswigger.net/web-security/cross-site-scripting/contexts/lab-canonical-link-tag)

This lab reflects user input in a canonical link tag and escapes angle brackets

Before starting this challenge, let’s go over some important knowledge we’ll need:
**what is canonical link :** It’s a special tag in a webpage that says “This is the **main** version of this page.” it looks like this `<link rel="canonical" href="https://example.com/page">`

**what is accesskey :** It lets you press a keyboard shortcut (like `Alt+Shift+x`) to **focus or "click"** that element.

Now we are ready to sole this challenge.
As we can see, the URL to this page is stored on the link tag below;

So we can inject  the following payload:
`'accesskey='x'onclick='alert(1)'`
When the user presses `ALT + SHIFT + X` it triggers `onclick` event and executes the alert.


