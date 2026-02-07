---
tags:
  - "#type/method"
  - "#attack/discovery"
---

---

> [!Hint] Comparison to [[1 Methods/Security-Testing/1 Reconnaissance/Overview - 1 Reconnaissance|Reconnaissance]] and [[1 Methods/Security-Testing/11 Collection/Overview - 11 Collection|Collection]].
> Discovery is typically **performed after an initial compromise to get some orientation within the target environment**. Collection is typically performed to enable a final impact. Reconnaissance is always performed from the outside of a target.

When we already are inside the targeted infrastructure, we either have a good C2 framework running, or must use tools that are available on the machine we are on. This limits the available techniques.

Very helpful ressource: "Living off the land binaries, scripts and libraries" (LOLBAS): <https://lolbas-project.github.io/>

# Shortlist of Tools

- DNS lookup with [[3 Tools/passive recon/nslookup|nslookup]]
- Port scan with [[3 Tools/shells/Netcat|Netcat]]
- Manual SMTP enumeration with [[2 Tech-Specifics/Network/Protocols/TCP 23 Telnet|TCP 23 Telnet]]
- Port scan with [[3 Tools/shells/PowerShell|PowerShell]]
- SMB enum on windows: [[3 Tools/network/SMB tools#net view|net view]]

# Attack Vectors

```base
filters:
  and:
    - file.tags.contains("#attack/discovery")
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

```

# Tools

```base
filters:
  and:
    - file.tags.contains("#attack/discovery")
    - file.tags.contains("#type/tool")
views:
  - type: table
    name: Table
    order:
      - file.name
      - Purpose

```
