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

Tools for Kerberos attacks typically already perform the necessary enumeration.

## Attacks

See:

- [[2 Tech-Specifics/Active Directory/Authentication Attacks/Active Directory Wordlist & Brute Force Attacks|Active Directory Wordlist & Brute Force Attacks]]
- [[2 Tech-Specifics/Active Directory/Authentication Attacks/dcsync Attack|dcsync Attack]]: high privileged user needed
- [[2 Tech-Specifics/Network/Protocols/TCP,UDP 88 Kerberos|Kerberos Attacks]]
	- [[2 Tech-Specifics/Network/Protocols/TCP,UDP 88 Kerberos#AS-REP Roasting|AS-REP Roasting]]: capture a users password hash
	- [[2 Tech-Specifics/Network/Protocols/TCP,UDP 88 Kerberos#Kerberoasting|Kerberoasting]]: capture a services password hash
	- [[2 Tech-Specifics/Network/Protocols/TCP,UDP 88 Kerberos#Silver Tickets|Silver Tickets]]: Forge a high-privileged service ticket

# Hardening
