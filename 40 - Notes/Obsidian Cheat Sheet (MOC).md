---
tags: [moc, topic/obsidian, topic/pkm, reference]
created: 2026-09-15
---

# Obsidian - Everything You Need to Know (Cheat Sheet)

> [!abstract] What this is
> A single practical reference for using Obsidian well: the mental model, the
> Markdown syntax, linking, the keyboard shortcuts that matter, and the handful
> of habits that make a vault actually useful. Everything here is either from
> the official Obsidian Help docs or standard defaults you can check yourself in
> **Settings -> Hotkeys**.

> [!tip] The two things to memorize first
> 1. **`Ctrl+P`** opens the **Command palette** - every command in Obsidian is
>    reachable here, and it shows the hotkey next to each command. If you forget
>    anything below, this is how you find it again.
> 2. **`Ctrl+O`** ("Quick switcher") jumps to any note by typing its name.
> On macOS use `Cmd` instead of `Ctrl` everywhere in this note.

---

## 1. The mental model

Obsidian is a Markdown editor over a **local folder of plain `.md` files** (your
"vault"). Nothing is locked in a database - your notes are just text files on
disk. Power comes from three things layered on top:

- **Links** `[[note]]` - connect notes into a graph. This is the core feature.
- **Tags** `#tag` - cross-cutting labels, independent of folders.
- **Plugins** - core (built-in, toggle on/off) and community (installed).

Structure is your choice: folders, links, tags, or a mix. See
[[Terraform Modules (MOC)]] for a worked example of a link-first knowledge set.

---

## 2. Essential keyboard shortcuts

> [!note] These are defaults
> Hotkeys are fully customizable in **Settings -> Hotkeys**, and displayed for a
> US keyboard layout. If one doesn't work, search the command in the Command
> palette (`Ctrl+P`) to see or set its key. On macOS swap `Ctrl` -> `Cmd`.

### Navigation & core
| Action | Shortcut |
|---|---|
| Command palette (do anything) | `Ctrl+P` |
| Quick switcher (open note by name) | `Ctrl+O` |
| Global / vault search | `Ctrl+Shift+F` |
| Search within current note | `Ctrl+F` |
| Open Settings | `Ctrl+,` |
| Create new note | `Ctrl+N` |
| Insert / follow a link | `Ctrl+K` (create), `Ctrl+Click` (open) |
| Open link in new pane | `Ctrl+Click` (or middle-click) |
| Go back / forward | `Alt+Left` / `Alt+Right` |
| Toggle left / right sidebar | `Ctrl+Alt+Left` / `Ctrl+Alt+Right` |

### Editing view & panes
| Action | Shortcut |
|---|---|
| Toggle Edit / Reading view | `Ctrl+E` |
| Split pane right | `Ctrl+Shift+\` (may be unset - assign it) |
| Close current pane/tab | `Ctrl+W` |
| Next / previous tab | `Ctrl+Tab` / `Ctrl+Shift+Tab` |
| Open graph view | (assign in Hotkeys, or Command palette) |

### Formatting (inside the editor)
| Action | Shortcut |
|---|---|
| Bold | `Ctrl+B` |
| Italic | `Ctrl+I` |
| Insert line break within a paragraph | `Shift+Enter` |
| Toggle checkbox / task | `Ctrl+L` (may be unset - assign it) |
| Fold / unfold heading or list | `Ctrl+Click` the fold arrow in the gutter |

> [!tip] Make your own
> The highest-value hotkeys to set yourself: "Insert template" (Templater),
> "Open today's daily note", "Toggle checkbox status", and "Add tag". Assign
> them in **Settings -> Hotkeys**.

---

## 3. Markdown formatting syntax

### Text styles
| Style | Syntax | Result |
|---|---|---|
| Bold | `**text**` or `__text__` | **text** |
| Italic | `*text*` or `_text_` | *text* |
| Bold + italic | `***text***` | ***text*** |
| Strikethrough | `~~text~~` | ~~text~~ |
| Highlight | `==text==` | ==text== |
| Inline code | `` `code` `` | `code` |
| Escape formatting | `\*not bold\*` | literal asterisks |

### Headings
```md
# H1
## H2
### H3   (up to ###### H6)
```
Headings feed the **Outline** panel and let you link to a specific section
(see linking below).

### Paragraphs & line breaks
- A **blank line** separates paragraphs.
- A single `Enter` continues the same paragraph in Reading view.
- To force a line break *within* a paragraph: end the line with **two spaces**,
  or press **`Shift+Enter`**.

### Lists, tasks, quotes
```md
- bullet
  - nested bullet
1. numbered
- [ ] unchecked task
- [x] done task

> a blockquote
```

### Code blocks
Fence with triple backticks and (optionally) a language for highlighting:
~~~md
```python
print("hello")
```
~~~

### Tables
```md
| Col A | Col B |
|-------|-------|
| a     | b     |
```

### Callouts (the boxed notes)
```md
> [!note] Optional title
> Body text.
```
Types include `note`, `tip`, `warning`, `info`, `success`, `question`,
`example`, `quote`, `abstract`, `danger`. Add a `-` after the type
(`> [!tip]-`) to make it **collapsible**.

---

## 4. Linking - the heart of Obsidian

| What | Syntax |
|---|---|
| Link to a note | `[[Note Name]]` |
| Link with display text | `[[Note Name\|shown text]]` |
| Link to a heading in a note | `[[Note Name#Heading]]` |
| Link to a block | `[[Note Name#^blockid]]` |
| **Embed/transclude** a note or section | `![[Note Name]]` or `![[Note#Heading]]` |
| Embed an image | `![[image.png]]` |
| External link | `[text](https://example.com)` |
| Tag | `#tag` or nested `#topic/subtopic` |

Tips:
- Type `[[` and Obsidian autocompletes existing note names.
- Linking to a note that **doesn't exist yet** creates a "dangling" link -
  click it later to create the note. Great for capturing TODO topics.
- **Backlinks** panel shows every note that links *to* the current one - this is
  how you rediscover connections.

---

## 5. Search operators (in global search)
| Operator | Finds |
|---|---|
| `tag:#project` | notes with a tag |
| `path:"20 - Literature"` | notes in a folder |
| `file:2026` | notes whose filename matches |
| `line:(term1 term2)` | both terms on the same line |
| `"exact phrase"` | exact phrase |
| `-term` | excludes a term |

---

## 6. Core plugins worth turning on
(Settings -> Core plugins)
- **Command palette**, **Quick switcher** - the two navigation workhorses.
- **Backlinks**, **Outgoing links** - see a note's connections.
- **Outline** - heading navigation for long notes.
- **Templates** / (community) **Templater** - reusable note skeletons.
- **Daily notes** / (community) **Periodic Notes** - journaling.
- **Graph view** - visualize the link graph.
- **Tag pane** - browse by tag.

Your vault already uses several community plugins (Dataview, Templater, Calendar,
Tasks, etc.) - see [[_SETUP GUIDE]].

---

## 7. Habits that make a vault actually good
- **Write atomic notes**: one idea per note. Small notes link better.
- **Link on first meaningful mention**, not everything - avoid link spam.
- **Use MOCs (Maps of Content)** as hand-made tables of contents for a topic,
  like [[Terraform Modules (MOC)]]. Links build structure; folders are optional.
- **Tags for themes, links for relationships.** `#security` is a theme; `[[TLS]]`
  is a relationship.
- **Capture dangling links freely** - they're your backlog of notes to write.
- **Revisit via Backlinks and Graph**, not by digging through folders.

---

## Related
- [[Terraform Modules (MOC)]] - example of a link-first knowledge set in this vault
- [[_SETUP GUIDE]] - this vault's plugins and workflow
- [[Home]] - dashboard

## Sources
- Obsidian Help. "Basic formatting syntax." https://help.obsidian.md/syntax (accessed 2026-09-15)
- Obsidian Help. "Hotkeys." https://help.obsidian.md/hotkeys (accessed 2026-09-15)
- Obsidian Help. "Internal links / Links." https://help.obsidian.md/links (accessed 2026-09-15)
