[[Write-ups/PortSwigger/XSS/Stored XSS/Overview|Stored XSS Overview]]
[[Write-ups/PortSwigger/XSS/Reflected XSS/Overview| Reflected XSS Overview]]

**DOM-based XSS**: is a type of XSS attack that occurs when a vulnerable web application modifies the DOM (Document Object Model) in the user's browser. This can happen, for example, when a user input is used to update the page's HTML or JavaScript code in some way. In a DOM-based XSS attack, the malicious code is not sent to the server, but is instead executed directly in the user's browser. This can make it difficult to detect and prevent these types of attacks, because the server does not have any record of the malicious code.

DOM-based XSS vulnerabilities usually arise when JavaScript takes data from an attacker-controllable source, such as the URL, and passes it to a sink that supports dynamic code execution, such as `eval()` or `innerHTML`. This enables attackers to execute malicious JavaScript, which typically allows them to hijack other users' accounts.

To deliver a DOM-based XSS attack, you need to place data into a source so that it is propagated to a sink and causes execution of arbitrary JavaScript.

The most common source for DOM XSS is the URL, which is typically accessed with the `window.location` object. An attacker can construct a link to send a victim to a vulnerable page with a payload in the query string and fragment portions of the URL. In certain circumstances, such as when targeting a 404 page or a website running PHP, the payload can also be placed in the path.

[[Write-ups/PortSwigger/XSS/DOM XSS/Write-Up 1|Write-Up 1]]
[[Write-ups/PortSwigger/XSS/DOM XSS/Write-Up 2|Write-Up 2]]
[[Write-ups/PortSwigger/XSS/DOM XSS/Write-Up 3|Write-Up 3]]
[[Write-ups/PortSwigger/XSS/DOM XSS/Write-Up 4|Write-Up 4]]
