---
tags:
  - todo
  - "#type/method"
---

Which techniques for executing code are possible very much depend on related technology and the type of [[1 Methods/Security-Testing/3 Initial Access/Overview - 3 Initial Access|Initial Access]] that has been achieved.

# Attack Vectors - Server Side

```base
filters:
  and:
    - file.tags.contains("#attack/execution/server-side")
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
    columnSize:
      file.name: 240

```

# Attack Vectors - Client Side

```base
filters:
  and:
    - '!file.tags.contains("#type/tool")'
    - file.tags.contains("#attack/execution/client-side")
formulas:
  Domain: file.folder.split("/")[1]
properties:
  formula.Domain:
    displayName: Technology
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
    - file.tags.contains("#attack/execution")
    - file.tags.contains("#type/tool")
views:
  - type: table
    name: Table
    order:
      - file.name
      - Purpose

```
