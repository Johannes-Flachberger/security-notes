---
tags:
  - "#type/method"
  - "#todo"
  - "#attack/collection"
---

---

# Attack Vectors

```base
filters:
  and:
    - file.tags.contains("#attack/collection")
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

```

# Tools

```base
filters:
  and:
    - file.tags.contains("#attack/collection")
    - file.tags.contains("#type/tool")
views:
  - type: table
    name: Table
    order:
      - file.name
      - Purpose
```
