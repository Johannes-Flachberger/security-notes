---
tags:
  - "#type/method"
  - attack/reconnaissance/active
---

Active recon makes contact with the target.

Gather as detailed information as possible about exposed services - here are notes about some usually exposed services

# Objective

Expand, enrich and deepen the knowledge gathered during passive recon.

**Workflow:**

1. Broadly enumerate the attack surface - this depends on the broad context and typically is one of the following:
	- [[2 Tech-Specifics/Network/Network Scanning|Network Scanning]]: most usual scenario
	- [[2 Tech-Specifics/Active Directory/Enumeration - AD/Overview - Enumeration - AD|Active Directory Enumeration]]
	- [[2 Tech-Specifics/Cloud/Reconnaissance - Cloud|Reconnaissance - Cloud]]
2. Enumerate each discovered service - see [[#Service Specific Enumeration]]
3. Perform [[2 Tech-Specifics/Network/Network-Based Vulnerability Scanning|Network-Based Vulnerability Scanning]]

# Service Specific Enumeration

```base
filters:
  and:
    - file.tags.contains("#attack/reconnaissance/active")
    - '!file.tags.contains("#type/tool")'
formulas:
  Domain: |
    file.folder.split("/")[1] + 
    if(file.folder.split("/")[2].isEmpty(),"", " / " + file.folder.split("/")[2]) 
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
