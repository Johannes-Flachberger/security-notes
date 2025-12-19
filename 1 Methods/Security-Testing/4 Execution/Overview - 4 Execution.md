---
tags:
  - type/note 
  - todo 
---
Which techniques for executing code are possible very much depend on related technology and the type of [[1 Methods/Security-Testing/3 Initial Access/Overview - 3 Initial Access|Initial Access]] that has been achieved.

# Attack Vectors - Server Side
```base
filters:
	and:
	- file.tags.contains("attack/execution/server-side")
    - '!file.tags.contains("type/tool")'
views:
- type: table
  name: Table
```
# Attack Vectors - Client Side
```base
filters:
	and:
	- file.tags.contains("attack/execution/client-side")
    - '!file.tags.contains("type/tool")'
views:
- type: table
  name: Table
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