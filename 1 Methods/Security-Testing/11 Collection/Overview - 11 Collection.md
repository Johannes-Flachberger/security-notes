---
tags:
  - "#type/method"
  - "#todo"
  - "#attack/collection"
---

---

> [!Hint] Comparison to [[1 Methods/Security-Testing/1 Reconnaissance/Overview - 1 Reconnaissance|Reconnaissance]] and [[1 Methods/Security-Testing/9 Discovery/Overview - 9 Discovery|Discovery]].
> Collection is typically **performed to enable a final impact**. Discovery is typically performed after an initial compromise to get some orientation within the target environment. Reconnaissance is always performed from the outside of a target.

# Attack Vectors

```base
filters:
  and:
    - file.tags.contains("#attack/collection")
    - '!file.tags.contains("#type/tool")'
formulas:
  Domain: file.folder.split("/")[1] + if(file.folder.split("/")[2].isEmpty(),"", " / " + file.folder.split("/")[2])
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
