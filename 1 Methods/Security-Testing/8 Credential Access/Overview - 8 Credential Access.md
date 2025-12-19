---
---
#todo 

# Attack Vectors
```base
filters:
	and:
	- file.tags.contains("#attack/credential-access")
    - '!file.tags.contains("#type/tool")'
views:
- type: table
  name: Table
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
