---
tags:
  - "#type/note"
---
# Fundamentals
client side attacks target a pure client machine, e.g. a business notebook.
since client machines are not directly accessible by technical means, other transmission methods are required:
- USB Dropping
- Watering Whole Attacks (also consider company internal ressources)
- Malicious files
Most of these initial access vectors rely on user some sort of user action, which can be provoked e.g. using [[2 Tech-Specifics/People/Phishing|Phishing]].

To support this, client side attacks are typically preceded by [[1 Methods/Security-Testing/1 Reconnaissance/Passive Recon/Overview - Passive Recon|Passive Recon]].
# Attack vectors
```base
filters:
  and:
    - file.tags.contains("#attack/initial-access/client-side")
    - '!file.tags.contains("#type/tool")'
formulas:
  Domain: file.folder.split("/")[1]
properties:
  formula.Domain:
    displayName: Domain
views:
  - type: table
    name: Table

``` 
