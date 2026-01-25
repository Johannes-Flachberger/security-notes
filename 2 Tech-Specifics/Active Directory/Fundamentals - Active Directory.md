---
tags:
  - "#type/tech-specific"
---

"Active Directory Domain Services" is a technology to manage objects, such as fileshares, servers, endpoints, users, etc. on a network. On Active Directory instance can host multiple domains, organized into a domain tree, or domain forests.

# Basic Components

## Domain Controller

- Core management component of the domain.
- Typically acts as authoritative name server for the domain.

## Objects

- Almost everything in a domain is an object.
- e.g. users, groups, shares, computers, etc.

## Domain Admins

Possess the highest privileges within a domain. The "Enterprise Admin" group as administrator privileges across all domain forests within an AD environment

## Service Principal Names (SPN)

Some (complex) applications dont run with a local service account, but instead are integrated into active directory. Each of those has a unique [Service Prinicipal Name](https|//learn.microsoft.com/en-us/windows/win32/ad/service-principal-names) (SPN) that associates the service with a service account. SPNs reveal IP address / domain name & ports of the running service.

# Object permissions

Each object in active directory (e.g. a file share) has an [Access Control List](https|//learn.microsoft.com/en-us/windows/win32/secauthz/access-control-lists) (ACL) that specifies which other object (e.g. users) have certain access rights on the object. ACLs consist on zero or more "Access Control Entries" (ACEs).

An ACE has lots of entries, however the most important are:

- `ObjectSID`: the [[2 Tech-Specifics/OS/Windows/Fundamentals - Windows#SIDs|SID]] of the object that can be accessed with the defined permissions
- `ActiveDirectoryRights`: the access rights that are granted
- `SecurityIdentifier`: the SID of the object (e.g. a group or user) the permissions are granted to

Active directory defines many different [access rights](https://learn.microsoft.com/en-us/windows/win32/secauthz/access-rights-and-access-masks) that can be used. The most important for pentesting are:

| Access right             | Purpose                               |
| ------------------------ | ------------------------------------- |
| `GenericAll`             | Full permissions on object            |
| `GenericWrite`           | Edit certain attributes on the object |
| `WriteOwner`             | Change ownership of the object        |
| `WriteDACL`              | Edit ACE's applied to object          |
| `AllExtendedRights`      | Change password, reset password, etc. |
| `ForceChangePassword`    | Password change for object            |
| `Self (Self-Membership)` | Add ourselves to e.g. a group         |

# Directory Replication

To enable redundancy, the directory database is usually replicated and synchronized across multiple domain controllers.

See:

- [Replication Overview](https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2003/cc772726(v=ws.10)?redirectedfrom=MSDN)
- [Directory Replication Service (DRS) Remote Protocol](https://learn.microsoft.com/en-us/openspecs/windows_protocols/ms-drsr/f977faaa-673e-4f66-b9bf-48c640241d47?redirectedfrom=MSDN)

Any object with the right privileges in the SID can request an update of directory data.

Using this feature, a domain controller can be "impersonated" and credentials can be accessed - see [[2 Tech-Specifics/Active Directory/Authentication Attacks/dcsync Attack|dcsync Attack]]
