#todo 

# Tech-Specific Attack Vectors
```query
tag:#tactic/collection  tag:#type/tech-specific 
```
# Tools
```base
filters:
  and:
    - file.tags.contains("#tactic/collection")
    - file.tags.contains("#type/tool")
views:
  - type: table
    name: Table 
```
