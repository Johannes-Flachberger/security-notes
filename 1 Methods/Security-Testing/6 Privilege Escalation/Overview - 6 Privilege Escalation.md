**Tags:** #type/method #tactic/privilege-escalation 

---

There are 2 types of privilege escalation:
horizontal: move between users on one level of privilege
vertical: gain additional privileges
# Attack Vectors
```query
tag:#tactic/privilege-escalation
-tag:#type/tool
-file:README
-file:"Overview - 6 Privilege Escalation"
```
# Tools
```base
filters:
  and:
    - file.tags.contains("#tactic/privilege-escalation")
    - file.tags.contains("#type/tool")
views:
  - type: table
    name: Table 
```