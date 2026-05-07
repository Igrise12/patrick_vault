# GDD Beginner Revamp Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Replace the current GDD template with a minimal living document built for a solo beginner — only essential sections present by default, optional sections hidden in collapsed callouts.

**Architecture:** Single file overwrite of `04_Templates/GDD (Game Design Document).md`. Always-present sections (Concept, Core Loop, Current Tasks, Dev Log) appear at the top. Optional sections (Key Features, Art & Audio, Story & World, Controls) are collapsed Obsidian `> [!note]-` callout blocks that don't clutter the view until needed.

**Tech Stack:** Obsidian (Templater plugin), Git

---

## Files

| Action | Path |
|---|---|
| Modify | `04_Templates/GDD (Game Design Document).md` |

---

## Task 1: Overwrite GDD Template

**Files:**
- Modify: `04_Templates/GDD (Game Design Document).md`

- [ ] **Step 1: Overwrite the file with the new template**

Write `/home/igrise/Obisidian/Vault/Patrick Home/04_Templates/GDD (Game Design Document).md` with this exact content:

```markdown
# 🎮 <% tp.file.title %>

**Engine:** 
**Genre:** 
**Status:** 🏗️ Prototyping
**Started:** <% tp.date.now("DD-MM-YYYY") %>

---

## Concept
*What is this game in one sentence?*

---

## Core Loop
*What does the player actually do, over and over?*

`Step 1` ➔ `Step 2` ➔ `Step 3`

---

## Current Tasks
- [ ] 

---

> [!note]- Optional: Key Features
> *What makes this game unique? List up to 3 features.*
> - 
> - 
> - 

> [!note]- Optional: Art & Audio
> *Art style, color palette, music mood, SFX notes.*
> - **Art Style:** 
> - **Color Palette:** 
> - **Music Mood:** 

> [!note]- Optional: Story & World
> *Only fill this if your game has a narrative.*
> - **Setting:** 
> - **Protagonist:** 
> - **Story Beat:** 

> [!note]- Optional: Controls
> *Finalize input mapping when you're ready.*
> | Action | Keyboard | Controller |
> | --- | --- | --- |
> | Move | WASD | Left Stick |
> | Jump | Space | Button South |
> | Attack | Left Click | Button West |

---

## Dev Log

### <% tp.date.now("DD-MM-YYYY") %>
*What did you build, decide, or learn today?*
```

- [ ] **Step 2: Verify Templater expressions are intact**

```bash
grep "tp\." "/home/igrise/Obisidian/Vault/Patrick Home/04_Templates/GDD (Game Design Document).md"
```

Expected output (3 lines):
```
# 🎮 <% tp.file.title %>
**Started:** <% tp.date.now("DD-MM-YYYY") %>
### <% tp.date.now("DD-MM-YYYY") %>
```

- [ ] **Step 3: Verify removed content is gone**

```bash
grep -i "executive\|berikan\|jelaskan\|development resources\|key takeaways\|narrative structure" "/home/igrise/Obisidian/Vault/Patrick Home/04_Templates/GDD (Game Design Document).md"
```

Expected: no output.

- [ ] **Step 4: Verify optional callouts are present**

```bash
grep "\[!note\]-" "/home/igrise/Obisidian/Vault/Patrick Home/04_Templates/GDD (Game Design Document).md"
```

Expected: 4 lines (one per optional section).

- [ ] **Step 5: Commit**

```bash
git -C "/home/igrise/Obisidian/Vault/Patrick Home" add "04_Templates/GDD (Game Design Document).md"
git -C "/home/igrise/Obisidian/Vault/Patrick Home" commit -m "feat: revamp GDD template for solo beginner — minimal living document with collapsed optional sections"
```

- [ ] **Step 6: Push**

```bash
git -C "/home/igrise/Obisidian/Vault/Patrick Home" push
```

Expected: `master -> master` push confirmation.
