# Design: Template Revamp & Project Management System

**Date:** 2026-05-07
**Vault:** Patrick Home (Obsidian)
**Status:** Approved

---

## Goal

Revamp all three existing templates for quality and consistency, and introduce a general-purpose project management system using a Hub + Milestone sub-notes architecture. Also add a structured Daily Note template and convert the root `Project Kanban.md` into a live Dataview dashboard.

---

## Architecture

### PM Model: Flat Milestone

```
01_Projects/
  <Project Name>/
    <Project Name>.md        ← Project Hub (uses Project Hub template)
    <Milestone Name>.md      ← Milestone Note (uses Milestone template)
    <Milestone Name>.md
    ...
```

All project notes live in the same folder. The Hub wikilinks to its Milestone notes. Dataview queries aggregate tasks across the vault.

---

## Templates

### 1. Project Hub (`04_Templates/Project Hub.md`)

**Frontmatter:**
- `project_name` — display name
- `status` — `Active | On Hold | Completed | Archived`
- `type` — `gamedev | study | personal | work | other`
- `start_date` — Templater auto-filled (DD-MM-YYYY)
- `due_date` — blank by default
- `tags` — user-defined

**Sections:**
- **Goal** — one paragraph describing the project's purpose and success criteria
- **Milestones** — bulleted wikilinks to Milestone notes; each line has a status emoji prefix (🔲 / 🔄 / ✅)
- **Quick Tasks** — inline task list for items too small to be a milestone
- **Active Tasks (Dataview)** — embedded query pulling all open `- [ ]` tasks from files in this folder
- **Notes** — freeform project notes, decisions, links

---

### 2. Milestone Note (`04_Templates/Milestone Note.md`)

**Frontmatter:**
- `project` — wikilink back to the Project Hub
- `milestone` — milestone name/number
- `status` — `Not Started | In Progress | Done`
- `due_date` — blank by default

**Sections:**
- **Goal** — one sentence describing what "done" looks like for this milestone
- **Tasks** — Obsidian Tasks-compatible checklist
- **Blockers** — anything preventing progress
- **Notes** — decisions, references, dev log entries

---

### 3. Daily Note (`04_Templates/Daily Note.md`)

Templater-powered. Created via Obsidian's Daily Notes core plugin pointing to `04_Templates/Daily Note.md`.

**Sections:**
- **Quick Capture** — freeform bullet list for anything that surfaces during the day
- **Today's Focus** — top 3 priorities as a checkbox list
- **Active Tasks (Dataview)** — query for all incomplete tasks from `01_Projects/` due today or with no date
- **End of Day** — reflection prompt (What got done? What's blocked? What moves to tomorrow?)

---

### 4. Atomic Zettel — Revamp (`04_Templates/Atomic Zettel (Concept Note).md`)

**Changes:**
- Add `source` field (where the idea came from)
- Add `status` field: `seedling | evergreen` (seedling = rough, evergreen = polished)
- Replace the bare `## Context` section with `## Background` for clarity
- Keep `## Core Concept` and `## Connections`

---

### 5. Resource Note — Revamp (`04_Templates/Resource Note.md`)

**Changes:**
- Add `date_processed` field (Templater auto-fill)
- Replace the single awkward table with three dedicated sections:
  - **Key Takeaways** — bulleted list
  - **Action Items** — task checklist
  - **Related Notes** — wikilinks to Zettel notes

---

### 6. GDD — Revamp (`04_Templates/GDD (Game Design Document).md`)

**Changes:**
- Remove all Indonesian filler placeholder text (e.g., "Berikan penjelasan singkat...")
- Replace fillers with concise English prompts in italics
- Keep all section headers and structure intact
- Remove the hardcoded project name "Zeldo: The Origin of Time" — use `{{title}}` Templater variable

---

## Project Kanban Dashboard

**File:** `Project Kanban.md` (vault root)

Replace the empty file with a Dataview-powered dashboard:
- Table of all notes in `01_Projects/` that have `status` frontmatter
- Columns: Project name, type, status, due_date
- Sorted by status (Active first), then due_date

---

## CLAUDE.md Update

Update the Templates table in CLAUDE.md to document the two new templates (Project Hub, Milestone Note, Daily Note) and the revamped frontmatter fields.

---

## Out of Scope

- No individual Task notes (task granularity stays at Milestone level)
- No sprint/velocity tracking
- No changes to folder structure beyond what's described above
