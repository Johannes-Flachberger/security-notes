
```base
filters:
  and:
    - file.tags.contains("#type/tool")
formulas:
  tactis: file.tags.filter(value.toString().contains("#tactic")).map(value)
  used by: file.backlinks.unique().length
properties:
  file.backlinks:
    displayName: used in
  formula.tactis:
    displayName: tactics
views:
  - type: table
    name: All
    order:
      - file.name
      - formula.used by
      - formula.tactis
    sort:
      - property: formula.used by
        direction: DESC
      - property: formula.tactis
        direction: DESC
      - property: file.name
        direction: ASC
    columnSize:
      file.name: 210
      formula.used by: 102
  - type: table
    name: Reconnaissance

```
