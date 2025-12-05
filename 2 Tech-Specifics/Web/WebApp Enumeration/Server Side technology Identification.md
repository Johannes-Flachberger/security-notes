**Tags:** #type/tech-specific #tactic/reconnaissance

---

Also known as web server fingerprinting/footprinting.
Discover the technology stack in use:
1. host OS
2. Web Server
3. Database
4. Front End & Back End framework
# Techniques:
## Wappalyzer
- passive & active
- browser extension that analyses websites, used frameworks,..
- reveals the whole technology stack: OS, UI frameworks, webservers, databases, javascript libraries,...
- [[3 Tools/web/Wappalyzer]]
## nmap
- active 
- Version scan reveals webserver
- `http-enum` script reveals interesting paths
## Inspect HTTP headers
- often returns information about the webserver version, used language,...
- `curl http://<IP> -v` 
- use developer tools of browser -> network tab
- Scanning
## Github
Search for open repos belonging to the target
## Netcraft
- passive
- analyse site report (icon to the right of the results)
- [[3 Tools/web/Netcraft|Netcraft]]
## Google hacking
[[8_unstructured/training/fhstp/2_semester/ASP/Recon_fingerprinting/Passive recon/Google Hacking|link]]
zero packet recon - search for files belong to the site, check filetype,...
## censys
[[3 Tools/passive recon/Censys.io]]
search for the webserver and then get info about services,versions,.. completely passively
