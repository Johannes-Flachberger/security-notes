---
---
#todo 

# Tech-Specific Attack Vectors
```base
filters:
	and:
	- file.tags.contains("tactic/defense-evasion")
    - '!file.tags.contains("type/tool")'
views:
- type: table
  name: Table
```
# Tools
```base
filters:
  and:
    - file.tags.contains("#tactic/defense-evasion")
    - file.tags.contains("#type/tool")
views:
  - type: table
    name: Table
    order:
      - file.name
      - Purpose
```