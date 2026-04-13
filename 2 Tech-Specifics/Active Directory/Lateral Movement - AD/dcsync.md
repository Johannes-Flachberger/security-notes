---
tags:
  - "#type/tech-specific"
  - "#attack/exfiltration"
  - "#attack/credential-access"
  - "#attack/persistence"
---
# Fundamentals

See [[2 Tech-Specifics/Active Directory/Fundamentals - AD|Fundamentals - AD]]

Exploiting the [[2 Tech-Specifics/Active Directory/Fundamentals - AD#Directory Replication|Directory Replication]] feature of active directory, a high-privileged attacker can impersonate a domain controller. Then, e.g. dump password hashes of any user in the domain.

**Further Reading:** [adsecurity](https://adsecurity.org/?p=2398#MimikatzDCSync)

# Pentesting

# Exfiltration & Credential Access

**Prerequisites:**

The following rights are necessary:

- Replicating Directory Changes
- Replicating Directory Changes All
- Replicating Directory Changes in Filtered Set

By default, these groups have the necessary right:

- Domain Admins
- Enterprise Admins
- Administrators

**Workflow:**

1. perform dcsync attack - e.g. extract password hashes
	- [[3 Tools/mimikatz#DCSync Attack|mimikatz]]: from domain-joined windows machine
	- [[3 Tools/network/impacket-scripts#Impacket-secretsdump|impacket-secretsdump]]: from non-domain joined machine (e.g. kali)
2. try to [[1 Methods/Security-Testing/3 Initial Access/Password Attacks#Local Attacks (Hash-cracking)|crack the obtained hashes]]
	- [[3 Tools/crypto/Hashcat|Hashcat]] mode 1000 "NTLM"

# Hardening
