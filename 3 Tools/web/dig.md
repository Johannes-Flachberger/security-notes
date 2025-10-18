**Tags:** #type/tool #tactic/reconnaissance/passive 
**Link:** https://linux.die.net/man/1/dig
**Purpose:** perfom DNS lookups 

---
# Info
DNS fundamentals: [[2 Tech-Specifics/Network/Protocols/DNS|DNS]]

alternative tool: `host` command in kali 
# Usage
`dig <@SERVER> DOMAIN_NAME <TYPE>`
-  SERVER is the DNS server that you want to query.
-  DOMAIN_NAME is the domain name you are looking up.
-  TYPE contains the DNS record type
eg. `dig tryhackme.com MX` 

types:
A=IPv4 adsresses
AAAA=IPv6 addresses
CNAME= Canonical Name
MX= Mail Servers
SOA= Start if Authority
TXT= TXT Records
