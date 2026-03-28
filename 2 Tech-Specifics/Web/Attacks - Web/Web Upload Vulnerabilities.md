---
tags:
  - "#type/tech-specific" 
  - "#attack/initial-access/server-side"  #attack/lateral-movement #attack/execution/server-side  
---
# Fundamentals

- Simplest form: upload a .php file to a webserver, which then gets executed by the server.
- Often, malicious file uploads can be combined with other vulnerabilities, e.g. [[2 Tech-Specifics/Web/Attacks - Web/OWASP TOP 10/xml external entity (XXE)|XXE]] or [[2 Tech-Specifics/Web/Attacks - Web/XSS Exploitation|XSS]]

**Attack Surface:**

- upload functionality of websites
	- attachments to blog posts, etc.
	- avatar images

# Pentesting

There are multiple possible attack vectors:

- Can you execute an uploaded file? --> Upload a [[1 Methods/Security-Testing/12 Command and Control/Remote Shells|webshell]]
- if uploaded files cannot be executed combine with [[2 Tech-Specifics/Web/Attacks - Web/Directory Traversal|Directory Traversal]] to overwrite [[2 Tech-Specifics/OS/Sensitive Files|Sensitive Files]] or other config files - e.g. the `.ssh/authorized_keys` file -> connect to the machine using ssh
- If the webserver server indicates if a file was already uploaded before: Brute force files on the server.
- Error messages might reveal information
- Windows Web servers might allow file uploads using [[2 Tech-Specifics/Network/Protocols/SMB|SMB]] --> insert an [[2 Tech-Specifics/OS/Windows/Fundamentals - Windows#UNC Paths|UNC path]] into the upload form

Often, uploaded files are filtered --> we need to bypass the filter:

---

## Filter Bypassing

**Workflow:** Try to probe/enumerate which kind of filters are set. - e.g. upload a text file and work from there, mutating the content

### Bypass Client Side Filtering

client side filtering often is done by javascript in your browser

Some basic ways to bypass:

1. turn off javascript in the browser
2. intercept and modify the incoming page or the file uploadeg with [[3 Tools/web/Burp Suite|Burp Suite]]
3. send file directly to upload endpoint - eg with [[3 Tools/web/cURL|cURL]]

### Bypass Server Side Filtering

various methods exist for file upload filtering, requiring various bypass techniques

#### Extension Filtering

- matches on the file extension
**Bypass:**
- use an alternate extension
	- Wikipedia lists possible extensions for each file format in the profile of each page - here is an overview: <https://en.wikipedia.org/wiki/List_of_file_formats>
- change extension to uppercase
- sometimes you can upoad the file with an allowed extension and then edit it to the needed extension (e.g. .php)

#### MIME Type Filtering

- Multipurpose Internet Mail Extension (MIME) types are used in the web to identify file types.
- MIME is based on file extension -> easy to bypass
**Bypass:**

#### Magic Number Validation

- magic number = a binary number at the beginning of every file that tells the file type
- might be faked, but is a little harder than extensions
- magic numbers by filetype <https://en.wikipedia.org/wiki/List_of_file_signatures>
**Bypass:**

#### Length Filtering

- typically not a problem for uploading shells

#### Name Filtering

- very usual, simple name sanitation
- files are renamed on upload

#### Content Filtering

- not done very common

# Hardening

Apply server side filtering for uploads
