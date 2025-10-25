**Tags:** #type/method #tactic/reconnaissance/active 

Active recon makes contact with the target.
Gather as detailed information as possible about exposed services - here are notes about some usually exposed services
# Objective
Expand, enrich and deepen the knowledge gathered during passive recon.
# Workflow
In general: start to enumerate the attack surface broadly (network &  port scanning)
then enumerate specific services
## 1. Port Scanning & Service Detection
See [[1 Methods/Security-Testing/1 Reconnaissance/Active/Port scanning|Port scanning]]
## 2. Vulnerability Scanning
See [[1 Methods/Security-Testing/1 Reconnaissance/Active/Vulnerability Scanning|Vulnerability Scanning]]
##  3. Web enumeration
See [[2 Tech-Specifics/Web/WebApp Enumeration/Overview - Web Application Enum|Overview - Web Application Enum]]
## 4. Enumerate each discovered network service
```query
tag:#tactic/reconnaissance/active path:"2 Tech-Specifics/Network"
```
# Tools
```query
tag:#tactic/reconnaissance/passive tag:#type/tool 
```









