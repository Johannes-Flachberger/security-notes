---
tags:
  - "#type/method"
---
In general, initial access can be achieved using
- [[1 Methods/Security-Testing/3 Initial Access/Server Side Attacks|Server Side Attacks]]
- [[1 Methods/Security-Testing/3 Initial Access/Client Side Attacks|Client Side Attacks]]
# Attack Vectors
```base
filters:
  and:
    - file.tags.contains("#attack/initial-access")
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
    sort: []
    columnSize:
      file.name: 237

```
# Tools
```base
filters:
  and:
    - file.tags.contains("#attack/initial-access")
    - file.tags.contains("#type/tool")
views:
  - type: table
    name: Table
    order:
      - file.name
      - Purpose

```
