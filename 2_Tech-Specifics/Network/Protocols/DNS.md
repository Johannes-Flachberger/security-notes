**Type:** #type/note
**Tags:** #todo 

---
Distributed database that translates domain names to IP addresses.

# Fundamentals
Each domain can use different types of DNS records. Some of the most common types of DNS records include:

- **NS**: Nameserver records contain the name of the authoritative servers hosting the DNS records for a domain.
- **A**: Also known as a host record, the "_a record_" contains the IPv4 address of a hostname (such as www.example.com).
- **AAAA**: Also known as a quad A host record, the "_aaaa record_" contains the IPv6 address of a hostname (such as www.example.com).
- **MX**: Mail Exchange records contain the names of the servers responsible for handling email for the domain. A domain can contain multiple MX records. Each MX record has a priority number. The server with the lowest priority number will be used first.
- **PTR**: Pointer Records are used in reverse lookup zones and can find the records associated with an IP address.
- **CNAME**: Canonical Name Records are used to create aliases for other host records.
- **TXT**: Text records can contain any arbitrary data and be used for various purposes, such as domain ownership verification.

**Zone Transfers** replicate data between DNS servers - they can leak internal data if misconfigurationa are present
# Pentesting
## Enumeration
- provides web & mail server addresses based on domains
- it is also worth checking the whole IP block of of the found ips with reverse enumeration
- txt records might reveal information
- zone transfers can leak internal data if misconfigured 
- tools: [[3_Tools/passive recon/DNS enumeration Tools|DNS enumeration Tools]]