**Type:** #type/theory
**Tags:**  #tactic/reconnaissance 

---
Here, both passive and active recon techniques are listed
[[3_Tools/web/Netcraft|Netcraft]] gives a good overview of a website including its technologies, etc.
[[3_Tools/web/Burp Suite|Burp Suite]] pro contains an excellent web app vulnerability scanner

> [!Note]
> Some webapps use their hostname in links and redirects --> if we want to bypass DNS or dont access to a DNS but prevent the links from braking we need to put the hostname in the `/etc/hosts` file. E.g. when testing VMs in isolate environments, hostnames might be used that are not listed in DNS.
> e.g. `cat "192.168.50.16 exampledomain" >> /etc/hosts` 

# Approach
1. Enumerate the technology stack
2. Enumerate the application
# Techniques
## Technology Identification
Discover the technology stack in use:
1. host OS
2. Web Server
3. Database
4. Front End & Back End framework
**Tools:**
- [[3_Tools/web/Wappalyzer|Wappalyzer]] - passive & active
	- reveals the whole technology stack: OS, UI frameworks, webservers, databases, javascript libraries,...
- [[3_Tools/web/Netcraft|Netcraft]] - passive
	- analyse site report (icon to the right of the results)  
- [[3_Tools/scanning/network/nmap]] - active 
	- Version scan reveals webserver
	- `http-enum` script reveals interesting paths
## Subdomain enumeration
- [[2_Tech-Specifics/Web/WebApp enum/Subdomain enumeration|Subdomain enumeration]]
## directory enumeration
wordlists: `/usr/share/wordlists/dirb/`
- [[3_Tools/web/gobuster|gobuster]] - active
	- dir mode
- nmap - script `http-enum`
- dirb - active
- dirbuster - active
- [[3_Tools/web/Photon|photon]]
## Analyse  HTTP Response Headers
analyse HTTP headers to get information about the websites security posture
Missing headers are not necessarily a vulnerablilty in itself, but they can be a sign that a webserver is poorly hardened
### Interesting headers
- `Server` Header can reveal Web Server Name and Version
- Headers prefixed with `X-` historically are used for non-standard headers and might reveal additional information 
**Ressources:**
- https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Headers
**Tools:**
- https://securityheaders.com/ - passive
- Browser Developer tools - network tab
## Analyse TLS config
https://www.ssllabs.com/ssltest/ - passive
analyses TLS configuration and compares against best practices - it can also detect some vulnerabiliities, e.g. Poodle or Heartbleed
## virtual hosts (vhost)
- [[3_Tools/web/gobuster|gobuster]]
- ffuf
## check metadata files
**Robots.txt**
- file that tells search engines which pages should not be shown
- may contain administration portals, hidden pages,....
- location: `http://<IP>/robots.txt`
**sitemap.xml**
- contains a sitemap -> all sites that shall be discoverable
- location: `http://<IP>/sitemap.xml`
## Debugging Page content
use developer tools of your browser

- File extension might reveal programming language
	- become less common, because web applications use the "route" concept
- Source code can reveal libraries & their versions, e.g. in comments
	- prettyfy javascript in developer settings
- Use "Inspect" function to check specific page elements
	- e.g inpect forms to find hidden additional form fields