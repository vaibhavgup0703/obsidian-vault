# Dashboard

## Open tasks
```tasks
not done
sort by due
limit 25
```

## Active projects
```dataview
TABLE status, created
FROM "Projects"
WHERE type = "project" AND status = "active"
SORT created DESC
```

## Recent notes
```dataview
TABLE file.mtime AS "Modified"
FROM ""
WHERE file.name != "Dashboard"
SORT file.mtime DESC
LIMIT 10
```
