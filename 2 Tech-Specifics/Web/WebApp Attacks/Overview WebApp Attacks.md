**Tags:** #type/tech-specific 

---
# Overview
[[2 Tech-Specifics/Web/OWASP TOP 10/Overview OWASP TOP 10|Overview OWASP TOP 10]] gives an overview of the most common webapp attack vectors. Altough frameworks use different technologies, they often apply the same principles - that leads to similar attack vectors across frameworks.

> [!NOTE]
> Browsers often optimize stuff for better UX -> this can get in the way when working with specifically crafted payloads. Better use [[3 Tools/web/cURL|cURL]] or [[3 Tools/web/Burp Suite|Burp Suite]]
# Cheatsheet
[[2 Tech-Specifics/Web/WebApp Attacks/Attacks/Webhacking Cheatsheet|Webhacking Cheatsheet]]
# Techniques
## Cross site scripting (XSS)
[[2 Tech-Specifics/Web/WebApp Attacks/Attacks/XSS Exploitation|XSS Exploitation]]
## Steal cookies
E.g. steal a session cookie 
This can be done e.g. using [[2 Tech-Specifics/Web/WebApp Attacks/Attacks/XSS Exploitation|XSS]], if [[2 Tech-Specifics/Web/WebApp Attacks/Attacks/Webhacking Cheatsheet#Cookies|relevant cookie flags]] are not set.
## Directory traversal
[[2 Tech-Specifics/Web/WebApp Attacks/Attacks/Directory Traversal|Directory Traversal]]
## File Inclusion
[[2 Tech-Specifics/Web/WebApp Attacks/Attacks/File Inclusion|File Inclusion]]
## Comman injection
[[2 Tech-Specifics/Web/WebApp Attacks/Attacks/Injection Attacks/Command Injection|Command Injection]]
## Upload Vulnerabilities

## Further ideas:
#todo 
Server Side request forgery by manipulating /etc/hosts or /etc/resolv.conf