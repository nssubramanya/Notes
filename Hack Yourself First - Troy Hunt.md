# Hack Yourself First - Troy Hunt

## Websites
[Vulenrable Website Link](hack-yourself-first.com)
Attacker website

## Tools
### Chrome
#### View Source
1. Menu->View Source
2. on Mac: Alt + Cmd + U

#### New Incognito Window
Shift + Cmd + N

#### Chrome Developer Tools
F12

1. Elements - Element to Screen & vice-versa
2. Resources - All Resources especially cookies (Name, Expiry, HTTP/S etc.)
3. Network - Network Requests List, Details (Request Headers, Request Method, Response Headers, Cookie details - Request & Response cookies)

#### Add Chrome Plugin - 'Edit This Cookie'

### Fiddler Web Debugger
* Acts as HTTP Proxy - sits in between HTTP Client and HTTP Server - can be used to simulate "Man-in-the-middle" attacker
* Capturing HTTP Requests
* View HTTP Request and Response Data
* Can Decrypt HTTPS Traffic when interacting with HTTPS sites - Uses self-signed certificate
* Provides a Composer where an existing HTTP Request can be Dragged & Dropped, Manipulated and Sent as a new Request
* Fiddler Script - Handle Events and alter code based on those events. For example, one can alter response from server before it reaches the browser and vice-versa.
* Fiddler Addons
* Addon intruder21

#### Fiddler on Mac
1. Download Mono and install
2. Download Fiddler and extract
3. Run the following

```
/Library/Frameworks/Mono.framework/Versions/Current/bin/mono --arch=32 Fiddler.exe
```

## Transport Layer Protection
### Objectives of Transport Layer Protection
1. Authenticity
2. Integrity
3. Confidentiality

#### Authenticity
1. Do we know who we're connecting to?
2. What guarantees can be made as to their identity?

#### Integrity
1. Can we trust that our requests have not been manipulated in transit?
2. Conversely, can we be confident that the responses haven't been modified?

Ensures No Man-in-the-middle attack

#### Confidentiality
1.  Can we be confident that data we're sending to the website is kept private in transit?
2. And again, conversely, are the responses sent to our browser being kept away from prying eyes?

### Understanding man in the middle attack
When somebody can intercept the communication between HTTP Client and HTTP Server either to just observe the transactions or to manipulate them

### How Request/Response Happens
Browser (or Any HTTP Client) <-> Router/Wireless Access Point <-> Wires (ADSL/Cable/Satellite) <-> ISP (Internet Service Provider) <-> Internet Nodes <-> Server (in Data Center)

Man in middle attack can happen between any of the above points of communication. Its very easy @ Wireless Router but difficult at ISP.

> Rule: 
> If there is ANY information whose Authenticity, Integrity and Confidentiality is important, it should be sent over HTTPS Connection.

### Protecting Sensitive Data in Transist
via HTTPS

#### Registration page demo

### User Registration Process
**How should User Registration be done?**

* What HTTP Methods must be used?
* How to send UserName, Password etc?
* What should be encrypted?
* How to use HTTPS?
* What should User Registration Return?
* What should User behavior be after this?
* What about authorization after authentication?
* What should be stored in DB?
* What if there are already other Users with same data that is being submitted?
* How to Re-direct non-secure HTTP requests to Secure HTTP URL?
* How does GET, POST work in HTTP and HTTPS?


### Cookies over HTTP
#### AuthCookie
* Authentication Cookie
* HTTP is stateless protocol
* Multiple HTTP Requests from a HTTP Client to a HTTP Server are un-related and Server does not keep any state. So, after successful authentication request, server does not remember that further requests from same client are still authenticated and associated with same client
* Auth Cookies s

#### Authentication Process
1. Client sends Login Request with Credentials (over secure connection)
2. Server authenticates creds against DB
3. Server returns Auth Cookie if auth is successful
Auth Cookie is unique for that user and should not be forgeable
4. Subsequent requests from HTTP Client need to attach the same Auth Cookie as part of further requests.  
5. Server can validate Cookie and identify user
6. Upon successful cookie validation, server processes the request and returns response

Note that for every request, the Auth Cookie has to be attached.

### Session Hijacking
Here, the attacker gets hold of the Auth Cookie, creates a new session with Server and creates the Auth Cookie in it. This way, the attacker gets authenticated automatically. 

Now attacher has hijacked the session and can do whatever the original authenticated user could have done!

### Mixed Mode Content
Its not just sufficient to load HTML via HTTP. Once authenticated, all resources (images, fonts, icons, 3rd party javascript, css etc.) from own site or cross-site must be loaded via HTTPS.

If not, an attacker could definitely manipulate any of these assets before content is rendered at the client.

#### Handling Mixed Mode content request
Use **Protocol Relative URLs** instead of hard-coding. The appropriate protocol is used to pull external content based on how the primary domain was loaded HTTP or HTTPS

Ex: <script src="//ajax.googleapis.com/ajax/libs/prototype/1.7.1.0/prototype.js">

Note:
Now that most websites are getting SSL enabled; it is recommended to use **https://** instead of **Protocol Relative URLs**

*Recommendation:* https://www.paulirish.com/2010/the-protocol-relative-url/

### HSTS - HTTP Strict Transport Security

HTTP Strict Transport Security (HSTS) is a web security policy mechanism that helps to protect websites against protocol downgrade attacks[1] and cookie hijacking. It allows web servers to declare that web browsers (or other complying user agents) should interact with it using only HTTPS connections, which provide Transport Layer Security (TLS/SSL), unlike the insecure HTTP protocol used alone.

Header that forces Strict HTTPS requests even if request is made on HTTP. It automatically issues a HTTPS request.

However, it is only implemented in Chrome and Firefox; not in safari & IE. So, support is partial.


