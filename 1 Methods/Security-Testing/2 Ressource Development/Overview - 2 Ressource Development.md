---
tags:
  - "#type/method"
---
# Wordlist generation
Generate wordlists for [[1 Methods/Security-Testing/8 Credential Access/Bruteforce and Dictionary Attacks|Bruteforce and Dictionary Attacks]].
Tools:
- [[3 Tools/bruteforce/CeWL|CeWL]]
- [[3 Tools/bruteforce/crunch|crunch]]
# Attack Vectors
```base
filters:
	and:
	- file.tags.contains("#attack/ressource-development")
	- '!file.tags.contains("#type/tool")'
views:
- type: table
  name: Table
```
# Tools
```base
filters:
  and:
    - file.tags.contains("#attack/ressource-development")
    - file.tags.contains("#type/tool")
views:
  - type: table
    name: Table
    order:
      - file.name
      - Purpose

```