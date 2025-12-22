---
tags:
  - "#type/tech-specific"
  - "#attack/reconnaissance/active"
  - "#attack/reconnaissance/passive"
---
A collection of techniques to enumerate subdomains.

> [!Tip] Tip: Generate wordlists using LLMs
> [[3 Tools/passive recon/LLM based OSINT|LLM based OSINT]]
# Techniques
## SSL/TLS Certificates
Databases exist that contain every actual and historical certificate for a domain name
- http://crt.sh/
- https://transparencyreport.google.com/https/certificates
## OSINT (open source intelligence)
- [[3 Tools/Google & Google Hacking|Google & Google Hacking]]
- zB. `site:*.tryhackme.com`
## DNS Bruteforce
- bruteforce possible subdomains per DNS requests
- tool: [[3 Tools/web/gobuster|gobuster]]
## Sublister
- tool for automated subdomain enumeration
- `./sublist3r.py -d <url>`
## [[3 Tools/web/Netcraft|Netcraft]]
passive enum
