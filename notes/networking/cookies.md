# Networking: Cookies

> small pieces of data stored on a users browser to help a web application maintain stateful information between different requests.

## Purpose

_Web applications are inherently stateless_ meaning that each request made to the server is independent of any previous requests. Every time the page refreshes or a new page is loaded the server has no knowledge of any previous interactions with the user. Cookies are used to maintain stateful information between different requests made by the same user.

**Typical Use Cases**:

- _authentication_: ensure users don't need to re-authenticate with every page reload.
- _preferences_: store user preferences like language or theme settings.
- _shopping carts_: keep track of items added to a cart across multiple pages.
- _analytics_: track user behavior for improving website performance and user experience.

## How Cookies Work

Cookies are set through _HTTP_ headers, either from the server to the client using the `Set-Cookie` header. When your browser receives the cookie, it will either keep track of it in memory (**temporary cookie**) or store it on disk in a small text file (**persistent cookie**).

When you return to a website that has previously set a cookie, your browser will check if the cookie is still valid (not expired) before creating an http request. If that condition is met the cookie is sent back to the server using the `Cookie` header. The server can then read the cookie and use the information stored within it to personalize your experience or maintain your session.

## Third-Party Cookies

_Third-party cookies_ are cookies that are sent to your browser from a different domain than the one you're currently visiting. These cookies are often used by advertisers and analytics services to build a database of your browsing habits across multiple websites.

**How are you sent third-party cookies?**

When you visit a website, it may include content from other domains, such as ads or social media widgets. Or even something as simple as: `<img src="trackers.ca/cat.png">`. These third-party domains can set their own cookies on your browser when their content is loaded. Anytime you visit a page that makes a request to a third-party domain, your browser may send any cookies associated with that domain along with the request.

## Legal and Privacy Considerations

- General Data Protection Regulation (GDPR)
- California Consumer Privacy Act (CCPA)
- ePrivacy Directive (EU Cookie Law)
- Children's Online Privacy Protection Act (COPPA)
- Personal Information Protection and Electronic Documents Act (PIPEDA)
