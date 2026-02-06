---
tags:
  - "#type/tech-specific" 
  - "#attack/reconnaissance/passive"   
---
# Fundamentals

Distributed database that translates domain names to IP addresses. Each domain can use different types of DNS records.

## DNS Record Types

- **NS**: Nameserver records contain the name of the authoritative servers hosting the DNS records for a domain.
- **A**: Also known as a host record, the "_a record_" contains the IPv4 address of a hostname (such as <www.example.com>).
- **AAAA**: Also known as a quad A host record, the "_aaaa record_" contains the IPv6 address of a hostname (such as <www.example.com>).
- **MX**: Mail Exchange records contain the names of the servers responsible for handling email for the domain. A domain can contain multiple MX records. Each MX record has a priority number. The server with the lowest priority number will be used first.
- **PTR**: Pointer Records are used in reverse lookup zones and can find the records associated with an IP address.
- **CNAME**: Canonical Name Records are used to create aliases for other host records.
- **TXT**: Text records can contain any arbitrary data and be used for various purposes, such as domain ownership verification.

## Zone Transfers

Zone transfers replicate data between DNS servers - they can leak internal data if misconfigurations are present

## DNSSEC

(Domain Name System security Extensions)

- suite of specification for securing information provided by DNS
- maintains backwards compatibility
- data origin authentication & data integrity protection

# Pentesting

## Enumeration

**Look for:**

- registered web & mail servers and their addresses
- txt records might reveal descriptive information
- lookup name servers & to deduce who the domain is managed by - use [[3 Tools/passive recon/whois|whois]] for identifying the registrar
- [[#Zone Transfers]] can leak internal data if misconfigured
- Use reverse lookups to identify alternate domain names for an IP
	- e.g. AWS assigns a service-specific domain name to each public IP
- Since public IPs are organised in blocks, performing reverse lookups of ip addresses in the same IP block might reveal related domains.

**Tools - Automated Enum**
- **[Dnsenum](https://github.com/SparrowOchon/dnsenum2): IMO the best automated enum tool to use locally**
	- `dnsenum <DOMAIN> [--threads <num>]`
- [DNS Dumpster](https://dnsdumpster.com/)
	- online service
	- freemium
	- helps with subdomain enumeration
	- gives a lot of info in easy to read format

**Tools - Manual Enum**
- [[3 Tools/web/host|host]]: straightforward & simple
- [[3 Tools/web/dig|dig]]: shows the most info
- [[3 Tools/passive recon/nslookup|nslookup]]: per default available on windows

## Command and Control

Can be used to "smuggle" data into a network

1. set up a dns server
2. configure txt entries for a domain
3. query the dns server from a target --> txt entries are transferred to the target
