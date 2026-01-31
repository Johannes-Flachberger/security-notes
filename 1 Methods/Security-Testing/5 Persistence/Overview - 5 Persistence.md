---
tags:
  - "#type/method"
  - "#todo"
  - "#attack/persistence"
---

---

# Attack Vectors

```base
filters:
  and:
    - file.tags.contains("#attack/persistence")
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
    sort:
      - property: formula.Domain
        direction: ASC

```

# Tools

```base
filters:
  and:
    - file.tags.contains("#attack/persistence")
    - file.tags.contains("#type/tool")
views:
  - type: table
    name: Table 
	order:
	  - file.name
	  - Purpose
```
