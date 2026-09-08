# Vault Setup Guide

Your "whole life" Obsidian system: **work**, **literature/reading**, **film**, and **daily life** — all backed up to GitHub automatically.

---

## 1. Git backup (DONE - already automated)

The **Obsidian Git** plugin is installed, configured, and running:

- Auto-commit every **10 min**
- Auto-push every **10 min**
- Pull before push, and pull on startup
- Remote: `https://github.com/aghriiv/vault`

You don't need to touch git manually. Just write notes; they sync themselves.
(You can force a sync anytime: Command palette -> "Obsidian Git: Commit and push".)

---

## 2. Plugins to install

Open **Settings -> Community plugins -> Browse**, then install each of these
(search the exact name, click Install, then Enable):

| Plugin | What it does |
|---|---|
| **Dataview** | Powers all the dashboards (Home / Work / Reading / Film) |
| **Templater** | Makes the templates in `99 - Templates` auto-fill dates/titles |
| **Calendar** | Calendar sidebar for daily notes |
| **Periodic Notes** | Daily / weekly / monthly notes |
| **Tasks** | Due dates, recurring & queryable tasks |
| **Kanban** | Drag-and-drop project boards |
| **QuickAdd** | One-hotkey capture of task / note / film / book |
| **Media DB Plugin** | Auto-fetches FILM + TV metadata (poster, director, year) |
| **Book Search** | Auto-fetches BOOK metadata by title / ISBN |
| **Advanced Tables** | Easy markdown tables |
| **Excalidraw** | Sketches / mind maps |
| **Homepage** | Opens `Home` automatically on startup |
| **Natural Language Dates** | Type "next friday" -> real date link |

---

## 3. Plugin settings to set (2 minutes)

**Templater**
- Template folder location -> `99 - Templates`
- (Optional) Enable "Trigger Templater on new file creation"

**Periodic Notes**
- Enable Daily notes -> folder `01 - Daily`, template `99 - Templates/Daily Note`

**Calendar**
- Nothing required; it uses the Periodic Notes daily-note setting.

**Homepage**
- Set homepage to `Home`.

**Media DB Plugin** (films)
- New file location -> `30 - Film`
- Template file -> `99 - Templates/Film` (optional)

**Book Search** (books)
- New file location -> `20 - Literature`
- Template -> `99 - Templates/Book` (optional)

**Tasks / Kanban / Advanced Tables / Excalidraw** work out of the box.

---

## 4. Folder structure

```
01 - Daily/         <- daily notes
10 - Work/          <- projects + meetings (work life)
20 - Literature/    <- books / reading
30 - Film/          <- films & TV
40 - Notes/         <- general knowledge / evergreen notes
50 - People/        <- contacts / who-is-who
90 - Attachments/   <- images, PDFs, posters, covers
99 - Templates/     <- Daily / Work Project / Meeting / Film / Book
Home.md             <- your main dashboard (startup page)
Work Dashboard.md
Reading Dashboard.md
Film Dashboard.md
```

Tip: set **Settings -> Files & Links -> Default location for new attachments**
to `90 - Attachments` to keep things tidy.

---

## 5. Daily workflow

1. Open Obsidian -> lands on **Home** (thanks to Homepage plugin).
2. Click today's date in the **Calendar** -> creates a daily note from the template.
3. Capture things fast with **QuickAdd** (assign it a hotkey in Settings -> Hotkeys).
4. Add a film -> Media DB command -> search -> it drops a fully-filled note in `30 - Film`.
5. Add a book -> Book Search command -> same idea into `20 - Literature`.
6. Everything shows up automatically on the dashboards. Git syncs it all.

---

## 6. Recommended (optional) improvement

Your vault lives inside **OneDrive**. OneDrive + Git both syncing the same
`.git` folder can occasionally cause conflicts/corruption. For maximum safety,
consider moving the vault outside OneDrive and letting Git be the only sync tool.
Ask me and I'll move it for you cleanly.
