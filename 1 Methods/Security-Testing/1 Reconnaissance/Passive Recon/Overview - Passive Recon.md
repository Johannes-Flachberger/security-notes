---
tags:
  - "#type/method"
  - "#attack/reconnaissance/passive"
---

Uses publically available information without making contact with the target. eg. use DNS lookups to get general information & contact data of a given domain name.

Less strict interpretation: We can also make contact, but only like a normal user does. For example, we can register an account and poke around to get an unterstanding of the target.

# Goals:

- expand the attack surface of the target
- gather information for social engineering or password guessing

This file describes general recon techniques that can be used for organizations, individuals, etc. Also check technology specific recon notes:

- [[2 Tech-Specifics/Web/Enumeration - Web/Overview - Enumeration - Web|Overview - Enumeration - Web]]

# OSINT Framework

A framework of useful ressources: <https://osintframework.com/>

# Techniques

Regardless of the platform were information can be found, advanced search can be very powerful:

## Google Hacking/ Google Dorks

[[3 Tools/Google & Google Hacking|Google & Google Hacking]]

## LLM Based Recon

- always fact check
- be aware that LLM providers analyse queries and responses
- [[3 Tools/passive recon/LLM based OSINT|LLM based OSINT]]

## Whois Enumeration

Find contact data, name servers, etc.

Tool: [[3 Tools/passive recon/whois|whois]]

## DNS Enumeration

- [[2 Tech-Specifics/Network/Protocols/DNS#Enumeration|DNS Enumeration]]

## Code Repositories

- eg. [[3 Tools/web/Github search|Github search]], Gitlab, Github Gist, Source Forge
- Find accessible repos belonging to the target
	- then search through the repos for valuable information
		- identify used technologies, architectural patterns, errors, etc.
		- scan for credentials - see [[2 Tech-Specifics/Dev/git|git]]

## S3 Buckets

- check if the company has an s3 bucket
- `http://<company chosen name>.s3.amazonaws.com/`

## Social Media

- **Linkedin:** find people that work at a company, their role what their knowhow is
- facebook, instagram, etc.
- online forums

## Corporate Websites

- general info about a company
- startpoint for [[2 Tech-Specifics/Web/Enumeration - Web/Subdomain Enumeration|Subdomain Enumeration]]

## Job Boards

- what technologies does the company use?

## Advanced Search

**Advanced search features for many patforms:** <https://github.com/cipher387/Advanced-search-operators-list>

**Advanced search engines**

- [[3 Tools/passive recon/Shodan|Shodan]]: find internet connect (iot) devices
- [[3 Tools/passive recon/Censys.io|Censys]]: IoT search engine
- [[3 Tools/passive recon/Napalm FTP|Napalm FTP]]: find FTP servers

## Document Metadata

Documents contain metadata that might reveal software versions, configurations, or timestamps.

Find files online:

- using [[3 Tools/web/gobuster|gobuster]] `-x`
- using [[3 Tools/Google & Google Hacking|Google & Google Hacking]]
- manually

To extract metadata from a file:

- [[3 Tools/utilities/exiftool|exiftool]]

# Attack Vectors

```base
filters:
  and:
    - file.tags.contains("#attack/reconnaissance/passive")
    - '!file.tags.contains("#type/tool")'
formulas:
  Domain: file.folder.split("/")[1] + if(file.folder.split("/")[2].isEmpty(),"", " / " + file.folder.split("/")[2])
properties:
  formula.Domain:
    displayName: Domain
views:
  - type: table
    name: Table
    order:
      - file.name
      - formula.Domain
    sort:
      - property: formula.Domain
        direction: ASC

```

# Tools

```base
filters:
  and:
    - file.tags.contains("#attack/reconnaissance/passive")
    - file.tags.contains("#type/tool")
views:
  - type: table
    name: Table
    order:
      - file.name
      - Purpose

```
