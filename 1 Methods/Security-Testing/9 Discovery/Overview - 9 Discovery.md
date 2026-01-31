---
tags:
  - "#type/method"
  - "#attack/discovery"
---

---

When we already are inside the targeted infrastructure, we either have a good C2 framework running, or must use tools that are available on the machine we are on. This limits the available techniques.

Very helpful ressource: "Living off the land binaries, scripts and libraries" (LOLBAS): <https://lolbas-project.github.io/>

# Shortlist of Tools

- DNS lookup with [[3 Tools/passive recon/DNS enumeration Tools|nslookup]]
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
