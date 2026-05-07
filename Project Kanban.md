# Project Kanban

```dataview
TABLE status, type, due_date AS "Due Date"
FROM "01_Projects"
WHERE status != null
SORT status ASC, due_date ASC
```
