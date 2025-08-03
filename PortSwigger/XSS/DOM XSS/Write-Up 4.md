#DOM-XSS 

DOM XSS in jQuery selector sink using a hashchange event: [link](portswigger.net/web-security/cross-site-scripting/dom-based/lab-jquery-selector-hash-change-event)

This lab contains a DOM-based cross-site scripting vulnerability on the home page. It uses jQuery's `$()` selector function to auto-scroll to a given post, whose title is passed via the `location.hash` property.  