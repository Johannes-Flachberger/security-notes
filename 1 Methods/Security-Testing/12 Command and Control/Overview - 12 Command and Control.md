#todo 

# Tech-Specific Attack Vectors
```query
tag:#tactic/command-and-control  tag:#type/tech-specific 
```
# Tools
```base
filters:
  and:
    - file.tags.contains("#tactic/command-and-control")
    - file.tags.contains("#type/tool")
views:
  - type: table
    name: Table 
```