# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What This Is

This is Patrick's personal Obsidian vault — a knowledge management system, not a software project. There are no build steps, tests, or package managers. The primary interface is Obsidian itself; Claude Code assists via the MCP Obsidian tools (`mcp__obsidian__*`) available in this session.

## Vault Structure

The vault uses a numbered PARA-like folder system:

- `00_Inbox/` — unprocessed captures
- `01_Projects/` — active projects with their own subfolders
  - `01_Gamedev/01_Zelda_Like_Game/` — "Zeldo: The Origin of Time" (Godot, 2D Action/Adventure)
  - `01_Gamedev/02_God_Knight/` — "God Knight" (Godot, Pixel Art action game)
- `02_Zettelkasten/` — atomic concept notes (e.g., Japanese JLPT grammar)
- `03_Resources/` — processed references/clippings
- `04_Templates/` — Templater templates (do not edit frontmatter `{{` variables)
- `05_Archive/` — completed/inactive material
- `copilot/copilot-custom-prompts/` — Obsidian Copilot plugin custom slash commands

Daily notes are created at the vault root using date format `DD-MM-YYYY` (e.g., `2026-05-06.md`).

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

## Active Plugins

- **Dataview** — SQL-like queries embedded in notes (used in `Daily Focus.md` to surface open tasks)
- **Obsidian Tasks** — task tracking with checkboxes and completion dates
- **Templater** — template engine; `<% tp.date.now("DD MMMM YYYY") %>` syntax in templates
- **Obsidian Copilot** — AI assistant with custom slash commands in `copilot/copilot-custom-prompts/`
- **Calendar** — daily note navigation
- **Obsidian Git** — auto-commits and syncs the vault to `git@github.com:Igrise12/patrick_vault.git`

## Working with This Vault

Use the `mcp__obsidian__*` tools to read, write, search, and manage notes. Prefer these over raw file reads/writes to preserve Obsidian's internal state.

Key tools:
- `mcp__obsidian__read_note` / `mcp__obsidian__write_note` — read or create/overwrite a note
- `mcp__obsidian__patch_note` — append or prepend content to an existing note
- `mcp__obsidian__search_notes` — full-text search across the vault
- `mcp__obsidian__list_directory` — browse vault structure

## Language

Patrick writes notes in **Indonesian** (Bahasa Indonesia). Match this language when drafting note content unless he requests otherwise.
