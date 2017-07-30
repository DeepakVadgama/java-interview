## Web

### Resources

- [IP Address Basics](http://www.deepakvadgama.com/blog/ipaddress-basics-for-developers/)
- [HTTP Overview](https://developer.mozilla.org/en-US/docs/Web/HTTP/Overview)
- [HTTP Statuses](https://httpstatuses.com)
- [HTTP Caching](https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/http-caching)

### TCP

- Transmission Control Protocol
- Based on connections (involves 3-way handshake) 
- Guaranteed delivery of packets
- Flow/Congestion control
- 'TCP Fast Open' improves connection times
- Good for sites, applications etc. 

### UDP

- User Datagram Protocol
- Delivery not guaranteed
- Stateless, not connection based
- Doesn't support ordering (to be handled by application)
- Good for games, videos etc. 

### HTTP Verbs

- HEAD, OPTIONS, GET, POST, PUT, DELETE

### HTTP Caching

- **ETag**: Fingerprint of the resource (eg: MD5 checksum), to indicate if resource is changed. 
- **no-cache**: Cache but use only after re-validating if resource is updated.
- **no-store**: Do not cache, and re-download for each request. 
- **max-age**: Amount in seconds the resource can be cached. 
- **must-revalidate, max-age:30**: Re-use cache for 30 seconds, after that must revalidate. (This can avoid download if resource has not been changed even after 30 seconds)
- **Ideal**: Have html pages as no-cache, and rename all other resources with unique file name (like md5 checksum of the file). 

### [HTTP Statuses](https://httpstatuses.com)

- 200: Ok
- 400: Bad request
- 401: Not authenticated
- 403: Not authorized
- 404: Not found
- 500: Internal server error

### [HTTP Statuses in a nutshell](https://twitter.com/stevelosh/status/372740571749572610?lang=en)
- 20x: Success
- 30x: Redirection
- 40x: Client Error
- 50x: Server Error

### HTTP 2

- Why?: Top sites average 100 requests per page. Browsers allow max 6 connections. Min 35ms round trip per request. 80 byte header.
- No head of line blocking.
- Binary
- Header compression. Does not send repeated headers. 
- Priority based
- Prefetch
- Server Push

### HTTPS (TLS)

- Transport Layer Security 
- Server port 443
- Certificate: Public-Private key. Signed by Certificate Authority (Verisign, Symantec, Thawte etc). These well known CAs are shipped and managed by the browser.
- Additional handshake on top of TCP


### Security
- **Origin**: protocol + host + port
- **Same Origin Policy**: JavaScript can only access same origin. Can’t access other iframes. If you request JS from other origin the response cannot be read.
- **CORS (Cross Origin Resource Sharing)**: Allow to get JS/CSS from other origins. Important for API providers. 
- **CSRF (Cross Site Request Forgery)**: Request originates from cross-site (potentially malicious) site. Can be avoided by Synchronized Token Pattern: Store token in cookie (can be read only by origin site) and pass that token along with every request as HTTP Param or Header (X-CSRF-TOKEN).
- **XSS (Cross Site Scripting)**: Malicious scripts are injected into the HTML/JS resources. Can be avoided by escaping injected strings etc.



