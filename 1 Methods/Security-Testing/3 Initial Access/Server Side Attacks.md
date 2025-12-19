---
---
## Server Side Attacks
target a server, i.e a machine that exposes a service
e.g. attacking network services:
```base
filters:
	and:
	- file.tags.contains("attack/initial-access")
    - '!file.tags.contains("type/tool")'
views:
- type: table
  name: Table
```
