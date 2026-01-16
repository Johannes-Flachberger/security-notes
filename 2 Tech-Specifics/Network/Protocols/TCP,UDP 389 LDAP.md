---
tags:
  - "#type/tech-specific"
---
# Fundamentals

Lightweight directory access protocol

Default Port: 389

LDAP is used to access objects in directory services, i.e tree structured databases. [[#LDAP Paths]] are used to access specific ressources

**Further reading:**
- https://ldap.com/basic-ldap-concepts/

## Security

- By default not encrypted.
- TLS-secured variant: LDAPS - default port 636

# LDAP Paths / Distinguished Names

LDAP uses a path format to access objects in the directory tree. A complete path to an object is also called "distinguished name".

The directory tree hierarchy in a distinguished name is represented from right to left. It starts from the domain component, over groups/organiztional units (OUs) to the individual object.

**Example:**

```sh
CN=Stephanie,CN=Users,DC=corp,DC=com
```

- DC: "domain component" - root of the directory tree, distinguished name of the domain itself
- CN: "common name" - identifier of an object in the domain

**Ressources:**
- [RFC](https://www.rfc-editor.org/rfc/rfc2247.html)

# Pentesting

# Hardening
