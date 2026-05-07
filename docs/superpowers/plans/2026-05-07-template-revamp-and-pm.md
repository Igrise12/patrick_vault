# Template Revamp & PM System Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Revamp three existing Obsidian templates, add three new PM templates (Project Hub, Milestone Note, Daily Note), convert Project Kanban into a Dataview dashboard, initialize git, and push to the remote.

**Architecture:** Flat Milestone PM model — each project has one Hub note linked to per-milestone sub-notes, all stored in the same project folder. Dataview queries aggregate tasks dynamically. All templates use the Templater plugin (`<% %>` syntax).

**Tech Stack:** Obsidian (Templater, Dataview, Obsidian Tasks, Obsidian Git), Git

---

## Files

| Action | Path |
|---|---|
| Create | `04_Templates/Project Hub.md` |
| Create | `04_Templates/Milestone Note.md` |
| Create | `04_Templates/Daily Note.md` |
| Modify | `04_Templates/Atomic Zettel (Concept Note).md` |
| Modify | `04_Templates/Resource Note.md` |
| Modify | `04_Templates/GDD (Game Design Document).md` |
| Modify | `Project Kanban.md` |
| Modify | `CLAUDE.md` |

---

## Task 1: Initialize Git and Set Remote

**Files:** none (git setup only)

- [ ] **Step 1: Initialize git repo in the vault root**

```bash
cd "/home/igrise/Obisidian/Vault/Patrick Home"
git init
```

Expected output: `Initialized empty Git repository in /home/igrise/Obisidian/Vault/Patrick Home/.git/`

- [ ] **Step 2: Create a .gitignore**

Create `.gitignore` at the vault root with this content:

```
.obsidian/workspace.json
.obsidian/workspace-mobile.json
.trash/
.DS_Store
```

- [ ] **Step 3: Add the remote**

```bash
git remote add origin git@github.com:Igrise12/patrick_vault.git
```

Verify: `git remote -v` should show `origin git@github.com:Igrise12/patrick_vault.git`

- [ ] **Step 4: Stage and commit existing vault files**

```bash
git add -A
git commit -m "chore: initial vault commit"
```

---

## Task 2: Create Project Hub Template

**Files:**
- Create: `04_Templates/Project Hub.md`

- [ ] **Step 1: Write the file**

Create `04_Templates/Project Hub.md` with this exact content:

```markdown
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
```

- [ ] **Step 2: Verify the file exists and the Templater syntax is intact**

```bash
grep -c "tp\." "/home/igrise/Obisidian/Vault/Patrick Home/04_Templates/Project Hub.md"
```

Expected: `4` (four Templater expressions in the file)

- [ ] **Step 3: Commit**

```bash
git add "04_Templates/Project Hub.md"
git commit -m "feat: add Project Hub template"
```

---

## Task 3: Create Milestone Note Template

**Files:**
- Create: `04_Templates/Milestone Note.md`

- [ ] **Step 1: Write the file**

Create `04_Templates/Milestone Note.md` with this exact content:

```markdown
---
project: 
milestone: <% tp.file.title %>
status: Not Started
due_date: 
---

# <% tp.file.title %>

## Goal
*One sentence: what does "done" look like for this milestone?*

## Tasks
- [ ] 

## Blockers

## Notes
*Decisions, references, and dev log entries.*
```

- [ ] **Step 2: Verify**

```bash
grep "tp\." "/home/igrise/Obisidian/Vault/Patrick Home/04_Templates/Milestone Note.md"
```

Expected output shows two lines containing `tp.file.title`.

- [ ] **Step 3: Commit**

```bash
git add "04_Templates/Milestone Note.md"
git commit -m "feat: add Milestone Note template"
```

---

## Task 4: Create Daily Note Template

**Files:**
- Create: `04_Templates/Daily Note.md`

- [ ] **Step 1: Write the file**

Create `04_Templates/Daily Note.md` with this exact content:

```markdown
# <% tp.date.now("DD-MM-YYYY") %>

## Quick Capture

## Today's Focus
- [ ] 
- [ ] 
- [ ] 

## Active Tasks
```dataview
TASK
FROM "01_Projects"
WHERE !completed
SORT file.mtime DESC
LIMIT 15
```

## End of Day
**What got done?**

**What's blocked?**

**What moves to tomorrow?**
```

- [ ] **Step 2: Verify**

```bash
grep "tp\." "/home/igrise/Obisidian/Vault/Patrick Home/04_Templates/Daily Note.md"
```

Expected: one line with `tp.date.now`.

- [ ] **Step 3: Configure Daily Notes plugin to use the template**

Create or overwrite `.obsidian/daily-notes.json` with:

```json
{
  "template": "04_Templates/Daily Note",
  "folder": "",
  "format": "DD-MM-YYYY"
}
```

`folder` left blank keeps daily notes at the vault root (current behaviour). `format` matches the existing date format.

- [ ] **Step 4: Verify the config file**

```bash
cat "/home/igrise/Obisidian/Vault/Patrick Home/.obsidian/daily-notes.json"
```

Expected: the JSON above.

- [ ] **Step 5: Commit**

```bash
git add "04_Templates/Daily Note.md" .obsidian/daily-notes.json
git commit -m "feat: add Daily Note template and wire up Daily Notes plugin"
```

---

## Task 5: Revamp Atomic Zettel Template

**Files:**
- Modify: `04_Templates/Atomic Zettel (Concept Note).md`

- [ ] **Step 1: Replace the file with the revamped version**

Overwrite `04_Templates/Atomic Zettel (Concept Note).md` with:

```markdown
---
tags: 
date: <% tp.date.now("DD-MM-YYYY") %>
source: 
status: seedling
related_links: 
---

# <% tp.file.title %>

## Background
*Where does this idea come from? What context does it need?*

## Core Concept
*The single, distilled idea — one paragraph max.*

## Connections
*Links to related notes, contradictions, or extensions of this concept.*
```

- [ ] **Step 2: Verify the new fields exist**

```bash
grep -E "^source:|^status:" "/home/igrise/Obisidian/Vault/Patrick Home/04_Templates/Atomic Zettel (Concept Note).md"
```

Expected:
```
source: 
status: seedling
```

- [ ] **Step 3: Commit**

```bash
git add "04_Templates/Atomic Zettel (Concept Note).md"
git commit -m "feat: revamp Atomic Zettel template — add source/status fields, rename Context to Background"
```

---

## Task 6: Revamp Resource Note Template

**Files:**
- Modify: `04_Templates/Resource Note.md`

- [ ] **Step 1: Replace the file with the revamped version**

Overwrite `04_Templates/Resource Note.md` with:

```markdown
---
status: To-Process
topic: 
source_url: 
date_processed: <% tp.date.now("DD-MM-YYYY") %>
---

# <% tp.file.title %>

## Key Takeaways
- 

## Action Items
- [ ] 

## Related Notes
- 
```

- [ ] **Step 2: Verify the new field and sections exist**

```bash
grep -E "^date_processed:|## Key Takeaways|## Action Items|## Related Notes" "/home/igrise/Obisidian/Vault/Patrick Home/04_Templates/Resource Note.md"
```

Expected: four matching lines.

- [ ] **Step 3: Commit**

```bash
git add "04_Templates/Resource Note.md"
git commit -m "feat: revamp Resource Note template — add date_processed, replace table with sections"
```

---

## Task 7: Revamp GDD Template

**Files:**
- Modify: `04_Templates/GDD (Game Design Document).md`

- [ ] **Step 1: Replace the file with the revamped version**

Overwrite `04_Templates/GDD (Game Design Document).md` with:

```markdown
# 🎮 Game Design Document: <% tp.file.title %>
**Project Name:** <% tp.file.title %>
**Lead Designer:** [[Patrick]]
**Current Date:** <% tp.date.now("DD MMMM YYYY") %>
**Status:** 🏗️ In-Development / Prototyping

---

## 1. Executive Summary
> [!abstract] Elevator Pitch
> *A 1-2 sentence pitch that immediately hooks the reader.*

- **Genre:** *Primary / Secondary*
- **Target Audience:** *Who is this game for?*
- **Platform(s):** PC / Console / Mobile

---

## 2. Gameplay Mechanics
### Core Loop
`Explore` ➔ `Combat` ➔ `Reward` ➔ `Upgrade`
*(Adapt to match your actual game loop)*

### Player Controls
| Action | Input (PC) | Input (Controller) |
| --- | --- | --- |
| Movement | WASD | Left Stick |
| Interact | E | Button South |
| Attack | Left Click | Button West |

### Key Features
> [!todo] Feature Priority List
> | Feature Name | Description | Priority |
> | :--- | :--- | :--- |
> | | | High |
> | | | Medium |
> | | | Low |

---

## 3. Technical Specifications
- **Game Engine:** [[Godot]]
- **Version Control:** Git (GitHub/GitLab)
- **Art Style:** *e.g. 3D Low-Poly, 2D Pixel Art*
- **Audio Requirements:** SFX, Background Music (BGM)

---

## 4. Narrative and Setting
### 🌍 World Building
*Describe the setting, atmosphere, and world lore.*

### 👤 Characters
- **Protagonist:** *Main character details.*
- **Key NPCs:** *Important supporting characters.*

### 📜 Narrative Structure
*(Link to other files if needed)*

---

## 5. Development Resources
| Category | Tool Recommendation | Resource Link |
| :--- | :--- | :--- |
| **Engine** | Godot | [Link]() |
| **3D Modeling** | Blender | [Link]() |
| **2D Graphics** | Krita / Figma | [Link]() |
| **Documentation** | Obsidian | [Link]() |

---

## 6. Key Takeaways & Tasks
- [ ] **Prototype Early:** Test the core mechanic before building complex systems.
- [ ] **Community:** Check game dev forums/Discord for early feedback.
- [ ] **Reading:** Reference "The Art of Game Design" by Jesse Schell.

---
## 🛠️ Dev Log & Notes
*(Use this section for daily notes and quick ideas.)*
```

- [ ] **Step 2: Verify Indonesian filler text is gone**

```bash
grep -i "berikan\|jelaskan\|ganti\|gunakan\|tokoh\|sebelum\|cek\|referensi" "/home/igrise/Obisidian/Vault/Patrick Home/04_Templates/GDD (Game Design Document).md"
```

Expected: no output (zero matches).

- [ ] **Step 3: Verify Templater title is used instead of hardcoded project name**

```bash
grep "Zeldo" "/home/igrise/Obisidian/Vault/Patrick Home/04_Templates/GDD (Game Design Document).md"
```

Expected: no output.

- [ ] **Step 4: Commit**

```bash
git add "04_Templates/GDD (Game Design Document).md"
git commit -m "feat: revamp GDD template — remove Indonesian filler, use Templater title variable"
```

---

## Task 8: Convert Project Kanban to Dataview Dashboard

**Files:**
- Modify: `Project Kanban.md`

- [ ] **Step 1: Replace the file**

Overwrite `Project Kanban.md` with:

```markdown
# Project Kanban

```dataview
TABLE status, type, due_date AS "Due Date"
FROM "01_Projects"
WHERE status != null
SORT status ASC, due_date ASC
```
```

- [ ] **Step 2: Verify the Dataview block is present**

```bash
grep "dataview" "/home/igrise/Obisidian/Vault/Patrick Home/Project Kanban.md"
```

Expected: one line with `` ```dataview ``.

- [ ] **Step 3: Commit**

```bash
git add "Project Kanban.md"
git commit -m "feat: convert Project Kanban to live Dataview dashboard"
```

---

## Task 9: Update CLAUDE.md

**Files:**
- Modify: `CLAUDE.md`

- [ ] **Step 1: Replace the Note Templates section**

Find and replace the existing `## Note Templates` section in `CLAUDE.md` with:

```markdown
## Note Templates

Six templates live in `04_Templates/`:

| Template | Frontmatter fields | Purpose |
|---|---|---|
| `Project Hub.md` | `project_name`, `status`, `type`, `start_date`, `due_date`, `tags` | One per project; links to Milestone notes; includes Dataview task query |
| `Milestone Note.md` | `project`, `milestone`, `status`, `due_date` | One per milestone; task checklist + blockers |
| `Daily Note.md` | *(none — Templater only)* | Daily capture, focus, Dataview active tasks, end-of-day reflection |
| `Atomic Zettel (Concept Note).md` | `tags`, `date`, `source`, `status`, `related_links` | Single-concept permanent notes; `status` is `seedling` or `evergreen` |
| `Resource Note.md` | `status`, `topic`, `source_url`, `date_processed` | Processed references; `status` starts as `To-Process` |
| `GDD (Game Design Document).md` | *(none — Templater only)* | Game design documents for gamedev projects |

**PM model:** Each project lives in `01_Projects/<Project Name>/`. The Hub note links to Milestone notes in the same folder. `Project Kanban.md` at the vault root is a live Dataview table of all projects.
```

- [ ] **Step 2: Also update the Obsidian Git line to reflect git is now initialized**

Find this line:
```
- **Obsidian Git** — auto-commits and syncs the vault to a Git remote; the vault does not have a `.git` repo initialized yet
```

Replace with:
```
- **Obsidian Git** — auto-commits and syncs the vault to `git@github.com:Igrise12/patrick_vault.git`
```

- [ ] **Step 3: Verify the new template table is present**

```bash
grep "Project Hub\|Milestone Note\|Daily Note" "/home/igrise/Obisidian/Vault/Patrick Home/CLAUDE.md"
```

Expected: three matching lines.

- [ ] **Step 4: Commit**

```bash
git add CLAUDE.md
git commit -m "docs: update CLAUDE.md with new template set and PM model"
```

---

## Task 10: Push to Remote

- [ ] **Step 1: Verify all commits are in place**

```bash
git log --oneline
```

Expected: at least 9 commits visible (one per task above).

- [ ] **Step 2: Push to remote**

```bash
git push -u origin main
```

If the default branch is `master` instead of `main`, run:

```bash
git push -u origin master
```

Expected: output ending with `Branch 'main' set up to track remote branch 'main' from 'origin'.`
