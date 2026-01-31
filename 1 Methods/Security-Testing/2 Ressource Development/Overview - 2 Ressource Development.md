---
tags:
  - "#type/method"
  - "#attack/ressource-development"
---
# Wordlist Generation

Generate wordlists for [[1 Methods/Security-Testing/8 Credential Access/Bruteforce and Dictionary Attacks|Bruteforce and Dictionary Attacks]].

Tools:

- [[3 Tools/bruteforce/CeWL|CeWL]]
- [[3 Tools/bruteforce/crunch|crunch]]
- [[3 Tools/crypto/Hashcat|Hashcat]]

## Common Rules

Some effective rules are listed in `/usr/share/hashcat/rules`

- users add `1` to the password if numbers are required
- users capitalize the first character if capitalized characters are required
- users often rely on common special characters, such as `!`, `@`, `#`

# Attack Vectors

```base
filters:
  and:
    - file.tags.contains("#attack/ressource-development")
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
