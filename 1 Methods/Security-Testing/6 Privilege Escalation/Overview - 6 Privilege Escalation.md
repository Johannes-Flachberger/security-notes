---
tags:
  - "#type/method" 
  - "#attack/privilege-escalation" 
---

There are 2 types of privilege escalation:

1. horizontal: move between users on one level of privilege
2. vertical: gain additional privileges by
	- incorporate a privileged user
	- create a new privileged user

Before enumeration & attempting privilege escalation, evaluate if elevated privileges would enable further impacts in the given scenario. This is not always the case.

# Attack Vectors

```base
filters:
  and:
    - file.tags.contains("#attack/privilege-escalation")
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
    cardSize: 780

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
