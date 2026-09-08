---
type: dashboard
tags: [dashboard, literature]
---

# Reading Dashboard

## Currently reading
```dataview
TABLE author, year, started
FROM "20 - Literature"
WHERE type = "book" AND status = "reading"
SORT started ASC
```

## To read
```dataview
TABLE author, year, genres
FROM "20 - Literature"
WHERE type = "book" AND status = "to-read"
SORT file.ctime DESC
```

## Read (by rating)
```dataview
TABLE author, year, rating, finished
FROM "20 - Literature"
WHERE type = "book" AND status = "read"
SORT rating DESC, finished DESC
```

## Stats
```dataview
TABLE length(rows) AS Count
FROM "20 - Literature"
WHERE type = "book"
GROUP BY status
```
