**Type:** #type/method
**Tags:**  #tactic/reconnaissance/passive

---
Uses publically available information without making contact with the target. eg. use DNS lookups to get general information & contact data of a given domain name.
Less strict interpretation: We can also make contact, but only like a normal user does. For example, we can register an account and poke around to get an unterstanding of the target.
# Goals:
- expand the attack surface of the target
- gather information for social engineering or password guessing

This file describes general recon techniques that can be used for organizations, individuals, etc. Also check technology specific recon notes:
- [[2 Tech-Specifics/Web/WebApp Enumeration/Overview - Web Application Enum|Overview - Web Application Enum]]
# OSINT Framework
A framework of useful ressources: https://osintframework.com/
# Techniques
Regardless of the platform were information can be found, advanced search can be very powerful:
## Google Hacking/ Google Dorks
[[3 Tools/Google & Google Hacking|Google & Google Hacking]]
## LLM based recon
- always fact check
- be aware that LLM providers analyse queries and responses
- [[3 Tools/passive recon/LLM based OSINT|LLM based OSINT]]
## Whois enumeration
Find contact data, name servers, etc.
Tool: [[3 Tools/passive recon/whois|whois]]
## DNS Enumeration
- [[2 Tech-Specifics/Network/Protocols/DNS#Enumeration|DNS Enumeration]]
## Code repositories
- eg. [[3 Tools/web/Github search|Github search]], Gitlab, Github Gist, Source Forge
- Search for open repositories belonging to the target
	- then search through the files for valuable information
	- identify used technologies, architectural patterns, errors, etc.
- Automated Tools: [[3 Tools/passive recon/Trufflehog|Trufflehog]], Gitleaks
## S3 buckets
- check if the company has an s3 bucket
- `http://<company chosen name>.s3.amazonaws.com/`
## Social Media
- **Linkedin:** find people that work at a company, their role what their knowhow is 
- facebook, instagram, etc.
- online forums
## Corporate websites
- general info about a company
- startpoint for subdomain enumeration
## Job boards
- what technologies does the company use?
## Advanced Search
**Advanced search features for many patforms:** https://github.com/cipher387/Advanced-search-operators-list
**Advanced search engines**
- [[3 Tools/passive recon/Shodan|Shodan]]: find internet connect (iot) devices
- [[3 Tools/passive recon/Censys.io|Censys]]: IoT search engine
- [[3 Tools/passive recon/Napalm FTP|Napalm FTP]]: find FTP servers

## Tools
```query
tag:#tactic/reconnaissance/passive tag:#type/tool 
```




