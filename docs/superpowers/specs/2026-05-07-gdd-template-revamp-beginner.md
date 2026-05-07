# Design: GDD Template Revamp — Solo Beginner (Living Document)

**Date:** 2026-05-07
**Vault:** Patrick Home (Obsidian)
**Status:** Approved

---

## Goal

Replace the current GDD template with a living document optimized for a solo beginner game developer. The template must have near-zero overhead at game start and grow naturally as the project evolves — not front-load design decisions that a beginner can't yet answer.

---

## Design Principles

- **Start small, grow naturally.** Only Concept, Core Loop, Tasks, and Dev Log are required on day one. Everything else is an optional section added when the game reaches that stage.
- **No blank intimidation.** Sections the developer isn't ready for are hidden as collapsible callout blocks (Obsidian `> [!note]- Optional: ...`) rather than empty headers.
- **Actionable over exhaustive.** The GDD should answer "what am I building today?" not "what is every detail of this game?"
- **Dev Log is first-class.** For a living document, the log of decisions and progress is as important as the design spec itself.

---

## Template Structure

### Always-Present Sections (fill on day 1)

#### Header block
Templater-powered fields:
- `**Game Name:**` — `<% tp.file.title %>`
- `**Engine:**` — blank (user fills: Godot, Unity, etc.)
- `**Genre:**` — blank
- `**Status:**` — `🏗️ Prototyping` (progression: `🏗️ Prototyping` → `🎮 Alpha` → `✅ Released` → `🗄️ Archived`)
- `**Started:**` — `<% tp.date.now("DD-MM-YYYY") %>`

#### Concept
One sentence describing the game. Prompt: *"What is this game in one sentence?"*

#### Core Loop
The 2-3 step cycle the player repeats. Presented as a simple arrow chain:
`Step 1` ➔ `Step 2` ➔ `Step 3`
Prompt below: *"What does the player actually do, over and over?"*

#### Current Tasks
An Obsidian Tasks-compatible checklist. This is the active sprint — whatever the developer is building right now. No phase labels, no priority columns.

#### Dev Log
Reverse-chronological entries. Each entry is a date heading (`### DD-MM-YYYY`) followed by freeform notes. Prompt: *"What did you build, decide, or learn today?"*

---

### Optional Sections (collapsible, added when needed)

These are rendered as collapsed Obsidian callouts so they don't clutter the view but are ready to expand:

| Callout title | When to use |
|---|---|
| `Optional: Key Features` | When you know what makes the game unique (cap: 3 features) |
| `Optional: Art & Audio` | When you start working on visuals or sound |
| `Optional: Story & World` | Only if the game has a narrative |
| `Optional: Controls` | When you finalize input mapping |

Each callout contains a minimal prompt (one sentence), not a full table.

---

## What is Removed vs. Current GDD

| Removed | Reason |
|---|---|
| Controls table | Too premature; better added in Optional: Controls when finalized |
| Development Resources table | Noise; a beginner doesn't need a curated tools list |
| Narrative Structure task checkbox | Merged into Optional: Story & World |
| Feature Priority table (High/Med/Low) | Overkill for solo dev; replaced with a plain 3-item list |
| Key Takeaways & Tasks section | Redundant with Current Tasks |
| Executive Summary callout block | Replaced by simpler "Concept" one-liner |

---

## Out of Scope

- No version tracking or changelog
- No team/role fields (solo only)
- No platform-specific fields
