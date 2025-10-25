**Tags:** #type/tech-specific #tactic/initial-access #tactic/lateral-movement

---
# Overview
- Simplest form: upload a .php file to a webserver, which then gets executed by the server.
- Often, malicious file uploads can be combined with other vulnerabilities, e.g. [[2 Tech-Specifics/Web/OWASP TOP 10/xml external entity (XXE)|XXE]] or [[2 Tech-Specifics/Web/WebApp Attacks/Attacks/XSS Exploitation|XSS]]
- Entrypoint: upload functionality of websites
# Workflow
1. Try to probe/enumerate which kind of filters are set. - e.g. upload a text file before
## Filter Bypassing
### Bypass client side filtering
client side filtering often is done by javascript in your browser
Some basic ways to bypass:
1. turn off javascript in the browser
2. intercept and modify the incoming page or the file upload- eg with [[3 Tools/web/Burp Suite|Burp Suite]]
3. send file directly to upload endpoint - eg with [[3 Tools/web/cURL|cURL]]
### Bypass server side filtering
various methods exist for file upload filtering, requiring various bypass techniques
#### Extension filtering
- matches on the file extension
**Bypass:**
- use an alternate extension
	- Wikipedia lists possible extensions for each file format in the profile of each page - here is an overview: https://en.wikipedia.org/wiki/List_of_file_formats
- change extension to uppercase
#### MIME type filtering
- Multipurpose Internet Mail Extension (MIME) types are used in the web to identify file types.
- MIME is based on file extension -> easy to bypass
**Bypass:**
#### Magic number validation
- magic number = a binary number at the beginning of every file that tells the file type
- might be faked, but is a little harder than extensions
- magic numbers by filetype https://en.wikipedia.org/wiki/List_of_file_signatures
**Bypass:**
#### Length filtering
- typically not a problem for uploading shells
#### Name filtering
- very usual, simple name sanitation
- files are renamed on upload
#### Content filtering
- not done very common

