---
---

Server Side Attacks target a server, i.e a machine that exposes a service - the exact techniques most often are service specific.

## Password Attacks

1. Use / spray gathered credentials. - use [[3 Tools/bruteforce/netexec|netexec]] or [[3 Tools/bruteforce/Hydra|Hydra]]
2. Try default or weak credentials, like `admin:admin`, the service name as username & password.
3. Spray all possible combinations of gathered credentials - beware from account lockout!
	- Also try usernames as passwords.
4. Some services have specific techniques, e.g. anonymous login on [[2 Tech-Specifics/Network/Protocols/FTP|FTP]]
5. If nothing else works try using [[1 Methods/Security-Testing/3 Initial Access/Password Attacks|Password Attacks]].

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
