---
tags:
  - "#type/method"
  - "#todo"
  - "#attack/defense-evasion"
---

---

# Attack Vectors

```base
filters:
  and:
    - file.tags.contains("#attack/defense-evasion")
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
    - file.tags.contains("#attack/defense-evasion")
    - file.tags.contains("#type/tool")
views:
  - type: table
    name: Table
    order:
      - file.name
      - Purpose
```
