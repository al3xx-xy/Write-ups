[[Write-ups/XSS/Reflected XSS/Overview| Reflected XSS Overview]]
[[Write-ups/XSS/DOM XSS/Overview|DOM XSS Overview]]

## What is Stored XSS

Stored cross-site scripting (also known as second-order or persistent XSS) arises when an application receives data from an untrusted source and includes that data within its later HTTP responses in an unsafe way.

In a stored XSS attack, the malicious code is stored on the server, and is executed every time the vulnerable page is accessed. For example, an attacker could inject malicious code into a comment on a blog post. When other users view the blog post, the malicious code is executed in their browsers, allowing the attacker to perform various actions.

Suppose a website allows users to submit comments on blog posts, which are displayed to other users. Users submit comments using an HTTP request like the following:
`postId=3&comment=This+post+was+extremely+helpful.&name=Carlos+Montoya&email=carlos%40normal-user.net`

After this comment has been submitted, any user who visits the blog post will receive the following within the application's response:

`<p>This post was extremely helpful.</p>`

[[Write-ups/XSS/Stored XSS/Write-Up 1|Write-Up 1]]
[[Write-ups/XSS/Stored XSS/Write-Up 2|Write-Up 2]]
[[Write-ups/XSS/Stored XSS/Write-Up 3|Write-Up 3]]
