---
tags:
  - "#type/tech-specific"
  - attack/credential-access
---
# Fundamentals

See [[2 Tech-Specifics/Active Directory/Fundamentals - Active Directory|Fundamentals - Active Directory]]

Exploiting the [[2 Tech-Specifics/Active Directory/Fundamentals - Active Directory#Directory Replication|Directory Replication]] feature of active directory, a high-privileged attacker can impersonate a domain controller and dump password hashes of ANY user in the domain.

**Further Reading:** [adsecurity](https://adsecurity.org/?p=2398#MimikatzDCSync)

# Pentesting

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
1. perform dcsync attack to obtain password hashes
2. try to [[1 Methods/Security-Testing/8 Credential Access/Bruteforce and Dictionary Attacks#Local Attacks (Hash-cracking)|crack the obtained hashes]]
	- [[3 Tools/crypto/Hashcat|Hashcat]] mode 1000 "NTLM"

**Tools:**
- [[3 Tools/mimikatz|mimikatz]]: from domain-joined windows machine
- [[3 Tools/network/impacket-scripts#Impacket-secretsdump|impacket-secretsdump]]: from non-domain joined machine (e.g. kali)

# Hardening
