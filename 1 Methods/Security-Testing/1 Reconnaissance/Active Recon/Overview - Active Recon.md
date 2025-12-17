**Tags:** #type/method #tactic/reconnaissance/active 

Active recon makes contact with the target.
Gather as detailed information as possible about exposed services - here are notes about some usually exposed services
# Objective
Expand, enrich and deepen the knowledge gathered during passive recon.
# Workflow
In general: start to enumerate the attack surface broadly (network &  port scanning)
then enumerate specific services
## 1. Port Scanning & Service Detection
See [[1 Methods/Security-Testing/1 Reconnaissance/Active Recon/Port scanning|Port scanning]]
## 2. Vulnerability Scanning
See [[1 Methods/Security-Testing/1 Reconnaissance/Active Recon/Vulnerability Scanning|Vulnerability Scanning]]
##  3. Web enumeration
See [[2 Tech-Specifics/Web/WebApp Enumeration/Overview - WebApp Enumeration|Overview - WebApp Enumeration]]
## 4. Enumerate each discovered network service
```base
filters:
  and:
    - file.tags.contains("#tactic/reconnaissance/active")
    - file.path.contains("2 Tech-Specifics/Network")
views:
  - type: table
    name: Table

```
# Tools
```base
filters:
  and:
    - file.tags.contains("#tactic/reconnaissance/active")
    - file.tags.contains("#type/tool")
views:
  - type: table
    name: Table 
```
# Tech-Specific Attack vectors
```base
filters:
  and:
    - file.tags.contains("#tactic/reconnaissance/active")
    - file.tags.contains("#type/tech-specific")
views:
  - type: table
    name: Table 
```