---
tags:
  - tactic/initial-access
---
In general, initial access can be achieved using
- [[1 Methods/Security-Testing/3 Initial Access/Server Side Attacks|Server Side Attacks]]
- [[1 Methods/Security-Testing/3 Initial Access/Client Side Attacks|Client Side Attacks]]
# Attack Vectors
```base
filters:
	and:
	- file.tags.contains("tactic/initial-access")
	- '!file.tags.contains("type/tool")'
views:
- type: table
  name: Table
```
# Tools
```base
filters:
  and:
    - file.tags.contains("tactic/initial-access")
    - file.tags.contains("type/tool")
views:
  - type: table
    name: Table
    order:
      - file.name
      - Purpose

```