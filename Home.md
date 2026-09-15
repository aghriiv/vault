---
type: dashboard
tags: [dashboard]
---

# Home

> [!tip] Quick capture
> Use QuickAdd (hotkey) to add a task, note, film, or book fast.

## Today
```dataview
LIST
FROM "01 - Daily"
WHERE type = "daily"
SORT date DESC
LIMIT 3
```

## Active work projects
```dataview
TABLE status, priority, due
FROM "10 - Work"
WHERE type = "project" AND status = "active"
SORT priority ASC, due ASC
```

## Open tasks (due soon)
```dataview
TASK
WHERE !completed AND due
SORT due ASC
LIMIT 15
```

## Currently reading / watching
```dataview
TABLE type AS "", status
FROM "20 - Literature" OR "30 - Film"
WHERE status = "reading" OR status = "watching"
```

## Jump to
- [[Work Dashboard]]
- [[Reading Dashboard]]
- [[Film Dashboard]]
- [[99 - Templates/Daily Note|New daily note template]]

## Knowledge notes
- [[Obsidian Cheat Sheet (MOC)]] - shortcuts, syntax, linking & good habits
- [[Terraform Modules (MOC)]] - Terraform modules, variables, types, outputs & locals


