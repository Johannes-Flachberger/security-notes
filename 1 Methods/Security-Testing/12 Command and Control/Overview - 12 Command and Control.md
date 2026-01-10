---
tags:
  - "#type/method"
  - "#todo"
---

---

# Useful Tricks

Use [[1 Methods/Security-Testing/10 Lateral Movement/Port forwarding and Tunneling|Remote Port Forwarding]] to achieve access to services running on localhost of a target or behind a firewall, e.g. [[2 Tech-Specifics/Network/Protocols/TCP 3389 RDP|RDP]]

# Attack Vectors

```base
filters:
  and:
    - file.tags.contains("#attack/command-and-control")
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
    - file.tags.contains("#attack/command-and-control")
    - file.tags.contains("#type/tool")
views:
  - type: table
    name: Table
    order:
      - file.name
      - Purpose

```
