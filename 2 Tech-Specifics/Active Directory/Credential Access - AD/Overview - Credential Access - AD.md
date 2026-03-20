---
tags:
  - "#type/tech-specific"
  - "#attack/credential-access"
  - "#attack/lateral-movement"
---
# Fundamentals

See [[2 Tech-Specifics/Active Directory/Fundamentals - AD|Fundamentals - AD]]

# Pentesting

## Enumeration

Use [[2 Tech-Specifics/Active Directory/Enumeration - AD/Overview - Enumeration - AD|Active Directory Enumeration]] and [[2 Tech-Specifics/OS/Windows/Enumeration - Windows/Overview - Enumeration - Windows|Windows Enumeration]].

**Hint:** Tools for Kerberos attacks typically already perform the relevant enumeration.

## Attacks

See:

- [[2 Tech-Specifics/OS/Windows/Credential Access - Windows/Overview - Credential Access - Windows|Windows Credential Access]]
- [[2 Tech-Specifics/Active Directory/Credential Access - AD/Wordlist & Brute Force Attacks - AD Specifics|Wordlist & Brute Force Attacks - AD Specifics]]
- [[2 Tech-Specifics/Network/Protocols/Kerberos|Kerberos Attacks]]
	- [[2 Tech-Specifics/Network/Protocols/Kerberos#AS-REP Roasting|AS-REP Roasting]]: capture a users password hash
	- [[2 Tech-Specifics/Network/Protocols/Kerberos#Kerberoasting|Kerberoasting]]: capture password hash of a service account
	- [[2 Tech-Specifics/Network/Protocols/Kerberos#Silver Tickets|Silver Tickets]]: Forge a high-privileged service ticket
	- [[2 Tech-Specifics/Active Directory/Credential Access - AD/Overpass the Hash|Overpass the Hash]]: Create a Kerberos TGT from an NTLM hash

# Hardening
