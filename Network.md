###what happens when you type in a URL in browser
---
- browser checks cache; if requested object is in cache and is fresh, skip to #9
- browser asks OS for server's IP address
- OS makes a DNS lookup and replies the IP address to the browser
- browser opens a TCP connection to server (this step is much more complex with HTTPS)
- browser sends the HTTP request through TCP connection
- browser receives HTTP response and may close the TCP connection, or reuse it for another request
- browser checks if the response is a redirect (3xx result status codes), authorization request (401), error (4xx and 5xx), etc.; these are handled differently from normal responses (2xx)
- if cacheable, response is stored in cache
- browser decodes response (e.g. if it's gzipped)
- browser determines what to do with response (e.g. is it a HTML page, is it an image, is it a sound clip?)
- browser renders response, or offers a download dialog for unrecognized types



http://stackoverflow.com/questions/2092527/what-happens-when-you-type-in-a-url-in-browser
http://edusagar.com/articles/view/70/What-happens-when-you-type-a-URL-in-browser
