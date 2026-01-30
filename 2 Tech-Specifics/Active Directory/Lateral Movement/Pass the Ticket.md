---
tags:
  - "#type/tech-specific"
  - "#attack/lateral-movement"
---
# Fundamentals

A TGS ticket is bound to the SPN it was issued for, but not bound to a specific host. --> Once a valid TGS is obtained, you can export it and inject it into the cache of another client.

# Pentesting

If the obtained TGS belongs to the present user, no local admin privileges are required

1. Find a TGS
	- e.g. use [[2 Tech-Specifics/Active Directory/Credential Access/Overpass the Hash|Overpass the Hash]]
	- extract cached tickets using [[3 Tools/mimikatz|mimikatz]]
2. Export the TGS using [[3 Tools/mimikatz|mimikatz]]
3. On the machine/user context you want to use, inject the TGS into memory using [[3 Tools/mimikatz|mimikatz]]

# Hardening
