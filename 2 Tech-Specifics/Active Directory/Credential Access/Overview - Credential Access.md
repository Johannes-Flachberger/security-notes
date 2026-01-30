---
tags:
  - "#type/tech-specific"
  - "#attack/credential-access"
  - "#attack/lateral-movement"
---
# Fundamentals

See [[2 Tech-Specifics/Active Directory/Fundamentals - Active Directory|Fundamentals - Active Directory]]

# Pentesting

## Enumeration

Use [[2 Tech-Specifics/Active Directory/Enumeration/Overview - Enumeration|Active Directory Enumeration]] and [[2 Tech-Specifics/OS/Windows/Enumeration - Windows/Overview - Enumeration - Windows|Windows Enumeration]].

**Hint:** Tools for Kerberos attacks typically already perform the relevant enumeration.

## Attacks

See:

- [[2 Tech-Specifics/OS/Windows/Credential Access/Overview - Credential Access|Windows Credential Access]]
- [[2 Tech-Specifics/Active Directory/Credential Access/Active Directory Wordlist & Brute Force Attacks|Active Directory Wordlist & Brute Force Attacks]]
- [[2 Tech-Specifics/Network/Protocols/TCP,UDP 88 Kerberos|Kerberos Attacks]]
	- [[2 Tech-Specifics/Network/Protocols/TCP,UDP 88 Kerberos#AS-REP Roasting|AS-REP Roasting]]: capture a users password hash
	- [[2 Tech-Specifics/Network/Protocols/TCP,UDP 88 Kerberos#Kerberoasting|Kerberoasting]]: capture password hash of a service account
	- [[2 Tech-Specifics/Network/Protocols/TCP,UDP 88 Kerberos#Silver Tickets|Silver Tickets]]: Forge a high-privileged service ticket
	- [[2 Tech-Specifics/Active Directory/Credential Access/Overpass the Hash|Overpass the Hash]]: Create a Kerberos TGT from an NTLM hash

# Hardening
