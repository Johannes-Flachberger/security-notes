**Type:** #type/tool
**Tags:**  #tactic/reconnaissance/passive 
**Link:** https://en.wikipedia.org/wiki/WHOIS
**Purpose:** enumeration of domain registries

---
# Info
whois is a protocol that communicates with public databases which hold info about domain registration records
port 43

**contains the following info:**
 - registrar: the company that registered the domain name
 - registrant contact: may include name, phone number, email (who legally owns the domain)
 - administrative contact (the person managing administrative access)
 - technical contact (the person managing DNS, infrastructure, etc.)
 - creation update, expiration dates
 - name servers: each name server might point to a different IP 
 - domain status
Sometimes, information is redacted for privacy, often it is public because registrars charge a fee to redact whois entries.

> [!tip]
> Reverse queries are also possible. - just provide the ip as argument
# Usage
`whois [DOMAIN_NAME]`
`whois [IP_ADDRESS]`
`-h` to specify the host used for the lookup

