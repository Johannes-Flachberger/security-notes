tags: #type/theory #tactic/reconnaissance 

---
A collection of techniques to enumerate subdomains.

> [!Tip] Tip: Generate wordlists using LLMs
> [[1_Theory/Security-Testing/1_In/1 Reconnaissance/Passive/LLM based OSINT|LLM based OSINT]]
# Techniques
## SSL/TLS Certificates
Databases exist that contain every actual and historical certificate for a domain name
- http://crt.sh/
- https://transparencyreport.google.com/https/certificates
## OSINT (open source intelligence)
- [[3_Tools/Google Hacking|Google Hacking]]
- zB. `site:*.tryhackme.com`
## DNS Bruteforce
- bruteforce possible subdomains per DNS requests
- tool: [[3_Tools/web/gobuster|gobuster]]
## Sublister
- tool for automated subdomain enumeration
- `./sublist3r.py -d <url>`
## [[3_Tools/web/Netcraft|Netcraft]]
passive enum

# API enumeration
General methodology:
emumerate the available paths step by step
- e.g. you know that an API is served at `http:example.com/api/`.  
- start with enumerating everything below `.../api/`
- if you find `.../api/users/` continue with that level
APIs URL paths often contain version information - e.g. `.../api/users/v1`
--> we can use [[3_Tools/web/gobuster#^eab456|gobusters pattern feature]] to enumerate paths using such patterns
--> then use [[3_Tools/web/cURL|cURL]] to query the API
## Tips
- Carefully check error messages of the API. E.g. with a "user" API, this might detail if a certain path/endpoint does not exist or the user id is not found
- Conceptually, try to imagine all use cases and functions the API might have and try to abuse it - e.g. creating a new user vs. logging in or trying to register a admin user using an "admin key"

