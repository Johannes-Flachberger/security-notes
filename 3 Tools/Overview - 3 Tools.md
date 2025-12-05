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
      - property: formula.tactis
        direction: DESC
      - property: file.name
        direction: ASC
    columnSize:
      formula.used by: 103
  - type: table
    name: Reconnaissance

```
