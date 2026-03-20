---
tags:
  - "#type/method"
  - "#attack/discovery"
---

---

> [!Hint] Comparison to [[1 Methods/Security-Testing/1 Reconnaissance/Overview - 1 Reconnaissance|Reconnaissance]] and [[1 Methods/Security-Testing/11 Collection/Overview - 11 Collection|Collection]].
> Discovery is typically **performed after an initial compromise to get some orientation within the target environment**. Collection is typically performed to enable a final impact. Reconnaissance is always performed from the outside of a target.

When we already are inside the targeted infrastructure, you have several options:

1. use tools that are available on the target - see [LOLBAS](https://lolbas-project.github.io/)
2. use [[1 Methods/Security-Testing/10 Lateral Movement/Port forwarding and Tunneling|Port forwarding and Tunneling]] to enable [[1 Methods/Security-Testing/1 Reconnaissance/Active Recon/Overview - Active Recon|Active Recon]] techniques from your host
3. transfer tools to the target using [[1 Methods/Security-Testing/13 Exfiltration/Overview - 13 Exfiltration|Exfiltration]] techniques, then use [[1 Methods/Security-Testing/1 Reconnaissance/Active Recon/Overview - Active Recon|Active Recon]]
4. use a [[1 Methods/Security-Testing/12 Command and Control/Command and control frameworks|C2 framework]] with built-in enumeration capabilities

# Shortlist of Tools - Windows

- DNS lookup with [[3 Tools/passive recon/nslookup|nslookup]]
- Port scan with [[3 Tools/shells/Netcat|Netcat]]
- Manual SMTP enumeration with [[2 Tech-Specifics/Network/Protocols/Telnet|Telnet]]
- Port scan with [[3 Tools/shells/PowerShell|PowerShell]]
- SMB enum on windows: [[3 Tools/network/net (windows built-in)|net (windows built-in)]]

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
