---
project_name: <% tp.file.title %>
status: Active
type: other
start_date: <% tp.date.now("DD-MM-YYYY") %>
due_date: 
tags: 
---

# <% tp.file.title %>

## Goal
*Describe the project's purpose and what success looks like.*

## Milestones
- 🔲 [[Milestone Name]]

## Quick Tasks
- [ ] 

## Active Tasks
```dataview
TASK
FROM "<% tp.file.folder(true) %>"
WHERE !completed
```

## Notes
*Decisions, links, and freeform notes.*
