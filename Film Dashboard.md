---
type: dashboard
tags: [dashboard, film]
---

# Film Dashboard

## Watchlist
```dataview
TABLE director, year, genres
FROM "30 - Film"
WHERE type = "film" AND status = "watchlist"
SORT file.ctime DESC
```

## Currently watching
```dataview
TABLE director, year
FROM "30 - Film"
WHERE type = "film" AND status = "watching"
```

## Watched (by rating)
```dataview
TABLE director, year, rating, watched_date
FROM "30 - Film"
WHERE type = "film" AND status = "watched"
SORT rating DESC, watched_date DESC
```

## Stats
```dataview
TABLE length(rows) AS Count
FROM "30 - Film"
WHERE type = "film"
GROUP BY status
```
