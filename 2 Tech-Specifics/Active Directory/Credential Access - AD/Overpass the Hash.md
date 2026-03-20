---
tags:
  - "#type/tech-specific"
  - "#attack/credential-access"
---
# Fundamentals

**Further reading:** [Blackhat Paper](https://blackhat.com/docs/us-14/materials/us-14-Duckwall-Abusing-Microsoft-Kerberos-Sorry-You-Guys-Don't-Get-It-wp.pdf)

Essentially, upgrading a cached [[2 Tech-Specifics/_Other/Cryptography/Hashing fundamentals|NTLM password hash]] hash to a [[2 Tech-Specifics/Network/Protocols/Kerberos|Kerberos]] TGT

# Pentesting

**Prerequites:** Local admin privileges

**Workflow:**
1. Obtain a username and its NTLM password hash - see [[2 Tech-Specifics/Active Directory/Credential Access - AD/Overview - Credential Access - AD|Overview - Credential Access - AD]]
2. Use [[3 Tools/mimikatz|mimikatz]] to extract a cached NTLM hash
3. Use [[3 Tools/mimikatz#Spawn Process with cached Credentials|mimikatz]] to spawn a process as another user whose credentials are cached.
4. Trigger a [[2 Tech-Specifics/Network/Protocols/Kerberos|Kerberos]] authentication request, to obtain a TGT or a TGS of the impersonated user.
	- try to authenticate to any service in the domain - e.g. use `net use \\<hostname>` to attempt a connection to an [[2 Tech-Specifics/Network/Protocols/SMB|SMB]] share
5. Use TGT or TGS Ticket:
	1. Use the TGT to open a remote session from the local host - see [[2 Tech-Specifics/Active Directory/Lateral Movement - AD/Overview - Lateral Movement - AD|Active Directory Lateral Movement]]
	2. Use the TGS for [[2 Tech-Specifics/Active Directory/Lateral Movement - AD/Pass the Ticket|Pass the Ticket]]

# Hardening
