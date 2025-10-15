**Type:** #type/theory
**Tags:** #tactic/reconnaissance  

---
# Objective
Get as detailed information about the target as possible. Information gathering forms the basis of the whole pentest and is therefore crucial.

# Workflow
**Start With Passive Recon**
- start with [[1_Theory/Security-Testing/1_In/1 Reconnaissance/Passive/LLM based OSINT|LLM based OSINT]]
- get an overview of the target
- refine and enrich results with automated tooling: [[1_Theory/Security-Testing/1_In/1 Reconnaissance/Passive/0 Overview - Passive Recon - OSINT|0 Overview - Passive Recon - OSINT]]
- Detailed enumeration of interesting parts (eg. Website, Repos, linkedin,...)
**Proceed with Active  Recon**
- 
## Short checklist
-   **Organization Information**
	- Employee details
	- addresses and contact details
	- partner details
	- weblinks
	- web technologies
	- patents, trademarks, etc.

-   **Network Information**
	- Domains, sub-domains
	- network blocks
	- network topologies
	- trusted routers
	- firewalls
	- IP addresses of the reachable systems
	- the Whois record
	- DNS records
	- and other related information

-   **System Information**
	- Operating systems
	- web server OS
	- location of web servers
	- credentials
## Big Checklist
> [!Tip] Hint: Use this in prompts for LLMs

1. **Organizational Information**
- Company name and aliases
- Domain names and subdomains
- Publicly known IP address ranges
- Physical addresses and office locations
- Business structure and key departments
- Subsidiaries, partners, and third-party vendors

2. **Technical Infrastructure**
- Web servers and technologies used (e.g., Apache, Nginx, IIS)
- Application frameworks (e.g., WordPress, Django, React)
- SSL/TLS certificate details (issuer, expiration, subdomains)
- Public-facing applications and services
- DNS records (A, MX, TXT, CNAME, PTR)
- Email infrastructure (SPF, DKIM, DMARC records)
- WHOIS data (domain registration details)
- IP geolocation and hosting providers
- VPNs, firewalls, proxies, and load balancers

3. **Employee Information**
- Names, email addresses, job titles
- Phone numbers and office contact info
- LinkedIn profiles and social media activity
- Public GitHub repositories and commits
- Company email format (e.g., firstname.lastname@example.com)

4. **Network Information**
- Autonomous System Numbers (ASNs)
- IP address blocks (via WHOIS or BGP data)
- Open ports and services (via scanning)
- Cloud infrastructure (AWS, Azure, GCP usage)
- Internal naming conventions (revealed through misconfigured DNS or headers)

5. **Web and Application Footprint**
- Subdomains (via enumeration tools and services)
- Site structure and hidden directories (robots.txt, sitemap.xml)
- Public file shares or exposed backups
- JavaScript files (can reveal endpoints or API keys)
- Error messages and stack traces
- Login portals and authentication methods

6. **Vulnerabilities and Misconfigurations**
- Known CVEs related to discovered technologies
- Unpatched services and software versions
- Misconfigured services (e.g., open S3 buckets, exposed Git repos)
- Default credentials or poorly protected interfaces

7. **Social Engineering Vectors**
- Public events, campaigns, or internal initiatives
- Company culture (e.g., dress code, language)
- Job postings (can reveal tech stack, software used)
- Employee complaints or reviews (e.g., Glassdoor)
- Recent news or press releases

8. **Third-party and Supply Chain**
- Vendors used for HR, finance, IT, etc.
- Technologies or platforms used (e.g., Jira, Slack)
- Email or domain trust relationships
- Shared infrastructure or CDN providers

9. **Historical Data**
- Archived versions of websites (via Wayback Machine)
- Previously leaked credentials or breaches (HaveIBeenPwned, breach databases)
- Historical DNS or WHOIS records

# Tools
## Passive recon tools
```query
tag:#goal/recon/passive tag:#type/tool 
```
## Active recon tools
```query
tag:#goal/recon/active tag:#type/tool 
```
