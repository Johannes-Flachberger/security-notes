---
---
## Server Side Attacks

target a server, i.e a machine that exposes a service - the exact techniques usually are service specific.

> [!Hint]
> If nothing else works, never forget to try a [[1 Methods/Security-Testing/8 Credential Access/Overview - 8 Credential Access|Overview - 8 Credential Access]] using [[1 Methods/Security-Testing/8 Credential Access/Bruteforce and Dictionary Attacks|Bruteforce and Dictionary Attacks]].

# Tech-Specific:

```base
filters:
	and:
	- file.tags.contains("#attack/initial-access")
    - '!file.tags.contains("#type/tool")'
formulas:
  Domain: file.folder.split("/")[1] + if(file.folder.split("/")[2].isEmpty(),"", " / " + file.folder.split("/")[2]) 
properties:
  formula.Domain:
    displayName: Domain
views:
  - type: table
    name: Table
    order:
      - file.name
      - formula.Domain
    sort:
      - property: formula.Domain
        direction: ASC
    columnSize:
      file.name: 245
```
