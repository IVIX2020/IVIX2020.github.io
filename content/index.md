```base
views:
  - type: cards
    name: Table
    filters:
      and:
        - file.folder == "x/blog"
    order:
      - file.name
      - file.ctime
      - tags
      - description

```
