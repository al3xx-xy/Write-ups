#### What is SSRF
Server-side request forgery is a web security vulnerability that allows an attacker to cause the server-side application to make requests to an unintended location.

In a typical SSRF attack, the attacker might cause the server to make a connection to internal-only services within the organization's infrastructure. In other cases, they may be able to force the server to connect to arbitrary external systems. This could leak sensitive data, such as authorization credentials.

#### What is the impact of SSRF attacks
A successful SSRF attack can often result in unauthorized actions or access to data within the organization. This can be in the vulnerable application, or on other back-end systems that the application can communicate with. In some situations, the SSRF vulnerability might allow an attacker to perform arbitrary command execution.

1. **Access Internal Systems:**
    - The attacker can make your server talk to other servers **inside your network** (for example: `http://localhost:8000` or `http://internal-api/admin`).
    - These systems are often not protected because they are supposed to be "private."
2. **Steal Data:**
    - The attacker might use SSRF to read data that the server can access but regular users can’t (like cloud metadata: `http://169.254.169.254` on AWS).
3. **Run Commands:**
    - In some bad cases, if the internal service is weak, the attacker can **run commands on the server** (this is very dangerous).
4. **Use Server to Attack Others:**
    - The server might send requests to **external systems**, like trying to hack another website.
    - It looks like **your server is the attacker**, not the real hacker — so your company may get blamed.

Some applications only allow inputs that match, a whitelist of permitted values. The filter may look for a match at the beginning of the input, or contained within in it. You may be able to bypass this filter by exploiting inconsistencies in URL parsing

The URL specification contains a number of features that are likely to be overlooked when URLs implement ad-hoc parsing and validation using this method

**1 Use `@` to hide the real URL**

`https://safe-site.com:pass@evil.com`
Looks like it’s going to safe-site.com
But it actually goes to evil.com
Everything before the @ is just login info — the real host is after the @

**2 Use `#` to break the URL**

`https://evil.com#safe-site.com
The filter might see safe-site.com (after #)
But the browser/server only uses what's before the # → goes to evil.com

**3 Use subdomains to trick the filter**

`https://safe-site.evil.com`
Starts with safe-site
But it’s really a subdomain of evil.com, fully under attacker control

**4 Use URL encoding to hide characters**

`https://evil.com/%2e%2e/safe-site`
Looks weird
But when decoded, might bypass the filter and trick the system
You can even do double encoding like:
`%252e → becomes %2e → becomes .`

**5 Combine all the above**

Attackers can mix these tricks to create something like:
`https://safe-site:pass@evil.com#safe-site.com`
Looks safe
Actually goes to evil.com

#### What is blind SSRF?
Blind SSRF vulnerabilities arise when an application can be induced to issue a back-end HTTP request to a supplied URL, but the response from the back-end request is not returned in the application's front-end response.

The impact of blind SSRF vulnerabilities is often lower than fully informed SSRF vulnerabilities because of their one-way nature. They cannot be trivially exploited to retrieve sensitive data from back-end systems, although in some situations they can be exploited to achieve full remote code execution.