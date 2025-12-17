#todo 

# Tech-Specific Attack Vectors
```query
tag:#tactic/defense-evasion  tag:#type/tech-specific
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
```