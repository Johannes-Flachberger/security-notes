---
tags:
  - type/method
  - tactic/reconnaissance  
---
# Objective
Get as detailed information about the target as possible. Information gathering forms the basis of the whole pentest and is therefore crucial.
# Workflow
## 1. Start With [[1 Methods/Security-Testing/1 Reconnaissance/Passive Recon/Overview - Passive Recon|Passive Recon/OSINT]]
- start with [[3 Tools/passive recon/LLM based OSINT|LLM based OSINT]]
- get an overview of the target
- refine and enrich results with automated tooling: [[1 Methods/Security-Testing/1 Reconnaissance/Passive Recon/Overview - Passive Recon|Overview - Passive Recon]]
- Detailed enumeration of interesting parts (eg. Website, Repos, linkedin,...)

If you are able to directly access the machine over a network:
## 2. Proceed with [[1 Methods/Security-Testing/1 Reconnaissance/Active Recon/Overview - Active Recon|Active Recon]]

**Note:** Depending on the context, you may only be able to use passive recon, e.g. if there is no network connectivity to the target, or the target is a pure client machine.
# Checklists
> [!Tip] Hint: Use checklists in prompts for [[3 Tools/passive recon/LLM based OSINT|LLM based OSINT]]
- [[1 Methods/Security-Testing/1 Reconnaissance/Reconnaissance Checklist Short|Reconnaissance Checklist Short]]
- [[1 Methods/Security-Testing/1 Reconnaissance/Reconnaissance Checklist Long|Reconnaissance Checklist Long]]

