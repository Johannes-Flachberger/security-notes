**Tags:** #type/tool #tactic/reconnaissance/passive
**Link:** https://www.geeksforgeeks.org/linux-unix/host-command-in-linux-with-examples/
**Purpose:** manually send DNS queries, DNS enumeration

---
# Info

# Usage 
`host <domain name>
`-t` specify type of DNS request 

for reverse lookup: `host <IP address>

**brute-force subdomains script:**
`for domain in $(cat list.txt); do host $domain.example.com; done`
remove negative results from output
`for domain in $(cat /usr/share/seclists/Discovery/DNS/subdomains-top1million-20000.txt ); do host $domain.example.com; done | grep -v "NXDOMAIN"`

**reverse lookup ip block:**
`for domain in $(seq 200 254); do host 51.222.169.$ip; done | grep -v "not found"`

#todo idea: Write a script that first performes subdomain enumeration and then does a reverse lookup of all the ip blocks found and checks if there are more subdomains
