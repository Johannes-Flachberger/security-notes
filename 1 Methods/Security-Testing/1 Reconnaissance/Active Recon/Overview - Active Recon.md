---
tags:
  - "#type/method"
  - attack/reconnaissance/active
---
Active recon makes contact with the target.
Gather as detailed information as possible about exposed services - here are notes about some usually exposed services
# Objective
Expand, enrich and deepen the knowledge gathered during passive recon.
# Workflow
In general: start to enumerate the attack surface broadly (network &  port scanning)
then enumerate specific services
## 1. Port Scanning & Service Detection
See [[1 Methods/Security-Testing/1 Reconnaissance/Active Recon/Port scanning|Port scanning]]
## 2. Enumerate each discovered network service
```base
filters:
  and:
    - file.tags.contains("#attack/reconnaissance/active")
    - file.path.contains("2 Tech-Specifics/Network")
views:
  - type: table
    name: Table

```
## 3. Vulnerability Scanning
See [[1 Methods/Security-Testing/1 Reconnaissance/Active Recon/Vulnerability Scanning|Vulnerability Scanning]]
##  4. Web enumeration
See [[2 Tech-Specifics/Web/WebApp Enumeration/Overview - WebApp Enumeration|Overview - WebApp Enumeration]]

# Attack vectors
```base
filters:
  and:
    - file.tags.contains("#attack/reconnaissance/active")
    - '!file.tags.contains("#type/tool")'
formulas:
  Domain: file.folder.split("/")[1]
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
    - file.tags.contains("#attack/reconnaissance/active")
    - file.tags.contains("#type/tool")
views:
  - type: table
    name: Table
    order:
      - file.name
      - Purpose
    sort:
      - property: file.name
        direction: ASC
      - property: Purpose
        direction: ASC
    columnSize:
      file.name: 162

```
