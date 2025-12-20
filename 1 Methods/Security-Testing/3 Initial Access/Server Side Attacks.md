---
---
## Server Side Attacks
target a server, i.e a machine that exposes a service
e.g. attacking network services:
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
```
