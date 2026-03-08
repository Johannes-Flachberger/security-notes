---
tags:
  - "#type/tech-specific"
  - "#attack/reconnaissance/active"
  - "#attack/reconnaissance/passive"
---

Here, both passive and active recon techniques are listed

[[3 Tools/web/Netcraft|Netcraft]] gives a good overview of a website including its technologies, etc.

[[3 Tools/web/Burp Suite|Burp Suite]] pro contains an excellent web app vulnerability scanner

> [!Note]
> Some webapps use their hostname in links and redirects --> if we want to bypass DNS or dont have access to a DNS but prevent the links from braking we need to put the hostname in the `/etc/hosts` file. E.g. when testing VMs in isolate environments, hostnames might be used that are not listed in DNS.
> e.g. `cat "192.168.50.16 exampledomain" >> /etc/hosts`

# Workflow

1. Enumerate the technology stack
2. Enumerate the application

# Techniques

## Technology Identification

[[2 Tech-Specifics/Web/WebApp Enumeration/Server Side technology Identification|Server Side technology Identification]]

## Subdomain Enumeration

- [[2 Tech-Specifics/Web/WebApp Enumeration/Subdomain Enumeration|Subdomain Enumeration]]

## Directory Enumeration

### Wordlist Based

Can find hidden directories, but is not as efficient as crawling.

**Wordlists:**

- `/usr/share/wordlists/dirb/`
- `/usr/share/wordlists/dirbuster/`

**Tools:**

- [[3 Tools/web/gobuster|gobuster]] - active (fastest, most versatile)
- [[3 Tools/network/scanning/nmap|nmap]] - script `http-enum`
- dirbuster - active
- dirb - active (old, single threaded)

### Crawlers

More efficient than wordlist based but cannot find hidden directories (i.e. where no site links to)

- [[3 Tools/web/Photon|photon]]

## API Enumeration

[[2 Tech-Specifics/Web/Rest API|Rest API]]

## Analyse HTTP Response Headers

analyse HTTP headers to get information about the websites security posture

Missing headers are not necessarily a vulnerablilty in itself, but they can be a sign that a webserver is poorly hardened

### Interesting Headers

- `Server` Header can reveal Web Server Name and Version
- Headers prefixed with `X-` historically are used for non-standard headers and might reveal additional information
**Ressources:**
- <https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Headers>
**Tools:**
- <https://securityheaders.com/> - passive
- Browser Developer tools - network tab

## Analyse TLS Config

<https://www.ssllabs.com/ssltest/> - passive

analyses TLS configuration and compares against best practices - it can also detect some vulnerabiliities, e.g. Poodle or Heartbleed

## Virtual Hosts (vhost)

- [[3 Tools/web/gobuster|gobuster]]
- [[3 Tools/web/ffuf|ffuf]]

## Check Metadata Files

**Robots.txt**

- file that tells search engines which pages should not be shown
- may contain administration portals, hidden pages,....
- location: `http://<IP>/robots.txt`
**sitemap.xml**
- contains a sitemap -> all sites that shall be discoverable
- location: `http://<IP>/sitemap.xml`

## Debugging Page Content

use browser developer tools

- File extension might reveal programming language
	- become less common, because web applications use the "route" concept
- Source code can reveal libraries & their versions, e.g. in comments
	- prettify javascript in developer settings
- Use "Inspect" function to check specific page elements
	- e.g inpect forms to find hidden additional form fields
- Use the "network tab" to check the domains ressources are loaded from.
	- e.g. from cloud storage? --> this might be another target.

## Analyse Website Content

Extract relevant data from webpage contents, e.g. email addresses, access keys,...

Tools:

- [[3 Tools/web/Photon|Photon]]
