#todo 

# Tech-Specific Attack Vectors
```query
tag:#tactic/persistence  tag:#type/tech-specific 
```
# Tools
```base
filters:
  and:
    - file.tags.contains("#tactic/persistence")
    - file.tags.contains("#type/tool")
views:
  - type: table
    name: Table 
```