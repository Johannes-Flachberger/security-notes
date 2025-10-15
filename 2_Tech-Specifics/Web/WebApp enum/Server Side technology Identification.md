tags: #type/theory #tactic/reconnaissance

---

Also known as web server  fingerprinting/footprinting
# Techniques:
## Inspect HTTP headers

- often returns information about the webserver version, used language,...
- `curl http://<IP> -v` 
- use developer tools of browser -> network tab
- Scanning
## Github
Search for open repos belonging to the target
## Wappalyzer
- browser extension that analyses websites, used frameworks,..
- [[3_Tools/web/Wappalyzer]]
## Google hacking
[[8_unstructured/training/fhstp/2_semester/ASP/Recon_fingerprinting/Passive recon/Google Hacking|link]]
zero packet recon - search for files belong to the site, check filetype,...
## censys
[[3_Tools/passive recon/Censys.io]]
search for the webserver and then get info about services,versions,.. completely passively
