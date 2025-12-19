---
tags:
  - "#type/method" 
  - "#attack/privilege-escalation" 
---

There are 2 types of privilege escalation:
horizontal: move between users on one level of privilege
vertical: gain additional privileges
# Attack Vectors
```base
filters:
	and:
	- file.tags.contains("#attack/privilege-escalation")
    - '!file.tags.contains("#type/tool")'
views:
- type: table
  name: Table
```
# Tools
```base
filters:
  and:
    - file.tags.contains("#attack/privilege-escalation")
    - file.tags.contains("#type/tool")
views:
  - type: table
    name: Table
    order:
      - file.name
      - Purpose

```