**Tags:** #type/note #todo 

---
Which techniques for executing code are possible very much depend on related technology and the type of [[1 Methods/Security-Testing/3 Initial Access/Overview - 3 Initial Access|Initial Access]] that has been achieved.

# Tech-Specific Attack Vectors - Server Side
```query
tag:#tactic/execution/server-side  tag:#type/tech-specific 
```
# Tech-Specific Attack Vectors - Client Side
```query
tag:#tactic/execution/client-side  tag:#type/tech-specific 
```

# Tools
```base
filters:
  and:
    - file.tags.contains("#tactic/execution")
    - file.tags.contains("#type/tool")
views:
  - type: table
    name: Table 
```