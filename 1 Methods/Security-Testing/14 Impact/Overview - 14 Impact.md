#todo 

# Tech-Specific Attack Vectors
```query
tag:#tactic/impact  tag:#type/tech-specific 
```
# Tools
```base
filters:
  and:
    - file.tags.contains("#tactic/impact")
    - file.tags.contains("#type/tool")
views:
  - type: table
    name: Table 
```