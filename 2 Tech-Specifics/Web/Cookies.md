**Tags:** #type/tech-specific

---
# Fundamentals
[https://developer.mozilla.org/en-US/docs/Web/HTTP/Cookies](https://developer.mozilla.org/en-US/docs/Web/HTTP/Cookies)
## Relevant cookie flags
- `Secure`: Cookie can only be sent over encrypted connections
- `HttpOnly`: Browser denys javascript access to the cookie
	- If not set, the cookie can be read by javascript - e.g. to [[2 Tech-Specifics/Web/WebApp Attacks/Overview - WebApp Attacks#Steal cookies|Steal a cookie]] using [[2 Tech-Specifics/Web/OWASP TOP 10/XSS Fundamentals|XSS Fundamentals]]

# Pentesting
eg. steal session token to impersonate someone

# Hardening
