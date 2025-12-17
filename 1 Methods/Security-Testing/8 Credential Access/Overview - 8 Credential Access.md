#todo 

# Tech-Specific Attack Vectors
```query
tag:#tactic/credential-access  tag:#type/tech-specific 
```
# Tools
```base
filters:
  and:
    - file.tags.contains("#tactic/credential-access")
    - file.tags.contains("#type/tool")
views:
  - type: table
    name: Table 
```
