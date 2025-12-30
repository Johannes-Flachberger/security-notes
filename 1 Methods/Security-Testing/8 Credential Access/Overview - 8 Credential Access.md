---
tags:
  - "#type/method"
  - "#todo"
---

---

# Ressources

<https://scatteredsecrets.com/> is a service that monitors the web for password breaches - if you are the owner you can list your breached passwords.

# Attack Vectors

```base
filters:
  and:
    - file.tags.contains("#attack/credential-access")
    - '!file.tags.contains("#type/tool")'
formulas:
  Domain: file.folder.split("/")[1]
properties:
  formula.Domain:
    displayName: Domain
views:
  - type: table
    name: Table
    order:
      - file.name
      - formula.Domain
    sort:
      - property: formula.Domain
        direction: ASC

```

# Tools

```base
filters:
  and:
    - file.tags.contains("#attack/credential-access")
    - file.tags.contains("#type/tool")
views:
  - type: table
    name: Table
    order:
      - file.name
      - Purpose

```
