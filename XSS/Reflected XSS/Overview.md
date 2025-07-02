[[Write-ups/XSS/Stored XSS/Overview|Stored XSS Overview]]

## What is reflected cross-site scripting?

**Reflected XSS**: In a reflected XSS attack, the malicious code is embedded in a link that is sent to the victim. When the victim clicks on the link, the code is executed in their browser. For example, an attacker could create a link that contains malicious JavaScript, and send it to the victim in an email. When the victim clicks on the link, the JavaScript code is executed in their browser, allowing the attacker to perform various actions, such as stealing their login credentials.

Suppose a website has a search function which receives the user-supplied search term in a URL parameter:
`https://insecure-website.com/search?term=<script>Malicious Code</script>`
The application echoes the supplied search term in the response to this URL:
`<p>You searched for: Malicious Code</p>`


## Impact of reflected XSS attacks

If an attacker can control a script that is executed in the victim's browser, then they can typically fully compromise that user. Amongst other things, the attacker can:
* Perform any action within the application that the user can perform.
* View any information that the user is able to view.
* Modify any information that the user is able to modify.
* nitiate interactions with other application users, including malicious attacks, that will appear to originate from the initial victim user.

[[Write-ups/XSS/Reflected XSS/Write-Up 1]]
[[Write-ups/XSS/Reflected XSS/Write-Up 2]]
[[Write-ups/XSS/Reflected XSS/Write-Up 3]]
[[Write-ups/XSS/Reflected XSS/Write-Up 4]]
[[Write-ups/XSS/Reflected XSS/Write-Up 5]]
[[Write-Up 6]]
[[Write-Up 6]]
[[Write-Up 7]]
[[Write-Up 8]]
[[Write-Up 9]]
[[Write-Up 10]]

