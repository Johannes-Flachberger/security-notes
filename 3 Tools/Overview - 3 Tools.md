
```base
filters:
  and:
    - file.tags.contains("#type/tool")
formulas:
  tactis: file.tags.filter(value.toString().contains("#tactic")).map(value)
  used by: file.backlinks.unique().length + file.links.unique().length
properties:
  file.backlinks:
    displayName: used in
  formula.tactis:
    displayName: tactics
  formula.used by:
    displayName: links
views:
  - type: table
    name: All
    order:
      - file.name
      - formula.used by
      - Purpose
    sort:
      - property: formula.used by
        direction: DESC
      - property: Purpose
        direction: DESC
      - property: formula.tactis
        direction: DESC
      - property: file.name
        direction: ASC
    columnSize:
      file.name: 216
      formula.used by: 86
  - type: table
    name: Reconnaissance

```
