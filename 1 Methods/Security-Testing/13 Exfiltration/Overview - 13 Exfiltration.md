#todo 

# Tech-Specific Attack Vectors
```query
tag:#tactic/exfiltration  tag:#type/tech-specific 
```
# Tools
```base
filters:
  and:
    - file.tags.contains("#tactic/exfiltration")
    - file.tags.contains("#type/tool")
views:
  - type: table
    name: Table 
```