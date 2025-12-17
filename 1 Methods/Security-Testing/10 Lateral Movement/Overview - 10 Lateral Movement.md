#todo 

# Tech-Specific Attack Vectors
```query
tag:#tactic/lateral-movement  tag:#type/tech-specific 
```
# Tools
```base
filters:
  and:
    - file.tags.contains("#tactic/lateral-movement")
    - file.tags.contains("#type/tool")
views:
  - type: table
    name: Table 
```