---
type: dashboard
tags: [dashboard, work]
---

# Work Dashboard

## Active projects
```dataview
TABLE status, priority, start, due
FROM "10 - Work"
WHERE type = "project" AND status = "active"
SORT priority ASC, due ASC
```

## On hold / someday
```dataview
TABLE priority, due
FROM "10 - Work"
WHERE type = "project" AND status != "active" AND status != "done"
SORT priority ASC
```

## All open work tasks
```dataview
TASK
FROM "10 - Work"
WHERE !completed
GROUP BY file.link
SORT due ASC
```

## Recent meetings
```dataview
TABLE date, attendees, project
FROM "10 - Work"
WHERE type = "meeting"
SORT date DESC
LIMIT 10
```

## Completed projects
```dataview
LIST
FROM "10 - Work"
WHERE type = "project" AND status = "done"
SORT file.mtime DESC
```
