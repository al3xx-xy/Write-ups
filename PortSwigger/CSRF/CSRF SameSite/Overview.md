#### what is SameSite

SameSite is a browser security mechanism that determines when a website's cookies are included in requests originating from other websites.
#### What is a site in the context of SameSite cookies?

In the context of SameSite cookie restrictions, a site is defined as the top-level domain (TLD), usually something like `.com` or `.net`

#### What's the difference between a site and an origin

The difference between a site and an origin is their scope; a site encompasses multiple domain names, whereas an origin only includes one.

| **Request from**          | **Request to**             | **Same-site?** | **Same-origin?** |
| ------------------------- | -------------------------- | -------------- | ---------------- |
| `https://example.com`     | `https://example.com`      | YES            | YES              |
| `https://app.example.com` | `https://app.example.com`  | YES            | NO               |
| `https://example.com`     | `https://example.com:8080` | YES            | NO               |
| `https://example.com`     | `https://example.co.uk`    | NO             | NO               |

#### How does SameSite work?

Before the SameSite mechanism was introduced, browsers sent cookies in every request to the domain that issued them, even if the request was triggered by an unrelated third-party website. SameSite works by enabling browsers and website owners to limit which cross-site requests, if any, should include specific cookies. This can help to reduce users' exposure to CSRF attacks,

Developers can manually configure a restriction level for each cookie they set, giving them more control over when these cookies are used. To do this, they just have to include the `SameSite` attribute in the `Set-Cookie` response header, along with their preferred value:

```
Set-Cookie: session=0F8tgdOhi9ynR1M9wa3ODa; SameSite=Strict
```

If the website issuing the cookie doesn't explicitly set a `SameSite` attribute, Chrome automatically applies `Lax` restrictions by default.

#### Strict

If a cookie is set with the `SameSite=Strict` attribute, browsers will not send it in any cross-site requests. In simple terms, this means that if the target site for the request does not match the site currently shown in the browser's address bar, it will not include the cookie.

#### Lax

SameSite restrictions mean that browsers will send the cookie in cross-site requests, but only if both of the following conditions are met:

- The request uses the `GET` method.
    
- The request resulted from a top-level navigation by the user, such as clicking on a link.