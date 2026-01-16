---
tags:
  - "#type/tech-specific"
---

"Active Directory Domain Services" is a technology to manage objects, such as fileshares, servers, endpoints, users, etc. on a network. On Active Directory instance can host multiple domains, organized into a domain tree, or domain forests.

# Basic Components

**Domain Controller**

- Core management component of the domain.
- Typically acts as authoritative name server for the domain.
- There can be multiple DCs in a domain. However, one DC, the "Primary Domain Controller" (PDC) holds the most updated information and overrides others when resolving conflicts. See [Microsoft Learn](https://learn.microsoft.com/en-gb/troubleshoot/windows-server/active-directory/fsmo-roles)

**Objects**

- Almost everything in a domain is an object.
**Domain Admins**

Highest privileges within a domain. The "Enterprise Admin" group as administrator privileges across all domain forests within an AD environment

## LDAP Access

For LDAP fundamentals, see [[2 Tech-Specifics/Network/Protocols/TCP,UDP 389 LDAP|LDAP]].

Use the following path schema to access AD objects using LDAP:

```powershell
LDAP://HostName[:PortNumber][/DistinguishedName]
```

Also see: [Microsoft Learn](https://learn.microsoft.com/en-us/windows/win32/adsi/ldap-adspath?redirectedfrom=MSDN)
