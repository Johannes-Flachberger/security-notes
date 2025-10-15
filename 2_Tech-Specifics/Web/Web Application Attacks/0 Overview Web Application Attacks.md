**Type:** #type/theory
**Tags:** #goal/exploitation #todo 

---
# Overview
[[2_Tech-Specifics/Web/OWASP TOP 10/0 Overview OWASP TOP 10|0 Overview OWASP TOP 10]] gives an overview of the most common webapp attack vectors. Altough frameworks use different technologies, they often apply the same principles  - that leads to similar attack vectors across frameworks.

> [!NOTE]
> Browsers often optimize stuff for better UX -> this can get in the way when working with specifically crafted payloads. Better use [[3_Tools/web/cURL|cURL]] or [[3_Tools/web/Burp Suite|Burp Suite]]
# Cheatsheet
[[2_Tech-Specifics/Web/Fundamentals/Webhacking Cheatsheet|Webhacking Cheatsheet]]
# Techniques
## Cross site scripting (XSS)
[[2_Tech-Specifics/Web/OWASP TOP 10/XSS Fundamentals|XSS Fundamentals]]
[[2_Tech-Specifics/Web/Web Application Attacks/XSS Exploitation|XSS Exploitation]]
## Steal cookies
^c0c94a
E.g. steal a session cookie 
This can be done e.g. using [[2_Tech-Specifics/Web/OWASP TOP 10/XSS Fundamentals|XSS Fundamentals]], if [[2_Tech-Specifics/Web/Fundamentals/Webhacking Cheatsheet#^30cd96|relevant cookie flags]] are not set.
## Directory traversal / File Inclusion
[[2_Tech-Specifics/Web/Web Application Attacks/file inclusion|file inclusion]]
## Comman injection
[[2_Tech-Specifics/Web/Web Application Attacks/Command Injection|Command Injection]]
## Further ideas:
Server Side request forgery by manipulating /etc/hosts or /etc/resolv.conf