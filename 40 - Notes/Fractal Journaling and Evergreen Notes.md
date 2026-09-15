---
tags: [topic/obsidian, topic/pkm, concept]
created: 2026-09-15
source: https://stephango.com/vault
---

# Fractal Journaling and Evergreen Notes

> [!summary]
> The four mechanics that make Steph Ango's vault actually work day to day:
> (1) **empty daily notes** used only as anchors, (2) the **unique-note capture**
> (`YYYY-MM-DD HHmm`) plus the **fractal review** that rolls thoughts upward,
> (3) **evergreen notes** - the durable ideas that capture distills into, and
> (4) **Bases**, which turns a `categories` property into a live view. This is the
> methodology behind [[Steph Ango Vault System (MOC)]].

---

## 1. The methodology in one picture

The system is a **funnel that runs on time**:

```
capture (many, messy)            YYYY-MM-DD HHmm quick notes
        |  every few days
        v
weekly compile                   Weekly Review  (salient points pulled out)
        |  monthly
        v
monthly review                   themes become visible
        |  yearly
        v
yearly review                    the story of your year
        \
         \--> distilled ideas graduate into --> EVERGREEN NOTES (permanent)
```

You capture cheaply and constantly, then **review at widening intervals** (days ->
weeks -> months -> years). Each review throws away the noise and keeps the signal.
The keepers get promoted into evergreen notes. That is the whole method: *capture
low, review often, promote the best.*

> [!tip] Why it is called "fractal"
> Each level looks like the level below it - a review of reviews of reviews. You can
> zoom in to a single 3pm thought, or zoom out to "what did this year mean," and it is
> the same shape at every scale.

---

## 2. Daily notes he keeps empty

Steph's rule (verbatim): daily notes are

> "all named `YYYY-MM-DD.md`. I do not write anything in daily notes, they exist solely
> to be linked to from other entries."

**What that means and why it is clever:**

- A daily note is just an **anchor in time** - a page that *represents* a day.
- He does not journal *inside* it. Instead, other notes **link to** the date.
  Example: a photo, a meeting note, or a thought links back to `[[2026-09-15]]`.
- Because everything that happened on a day links to that date, the day's note gets a
  rich **Backlinks** panel automatically - a table of contents for the day that he
  never had to write by hand.
- Keeping them empty avoids the trap of "I must fill in my journal today." There is no
  blank page guilt; the day fills itself in from the things you actually did.

> [!note] In YOUR vault
> Your `01 - Daily` folder + the Periodic Notes plugin already create `YYYY-MM-DD` notes.
> You can use them either way - write in them, OR adopt Steph's "empty anchor" style and
> just link to dates. The Backlinks pane (Ctrl/Cmd+click the link, or the right sidebar)
> is where the value shows up.

---

## 3. The unique note: `YYYY-MM-DD HHmm`

This is the **capture** step and the part you asked about specifically.

- Obsidian has a command called **"Create new note"** / a *unique note* hotkey that makes
  a new note whose name is **stamped with the current date and time down to the minute**,
  e.g. `2026-09-15 1503`. (This is Obsidian's core **Unique note creator** feature; you set
  a format and a folder in Settings.)
- The timestamp guarantees the name is **always unique**, so you can fire off a thought
  instantly without stopping to name it. You *may* add a short title after the stamp, e.g.
  `2026-09-15 1503 idea about caching`.
- One note = **one thought**. Link people/things with `[[ ]]` even if those notes do not
  exist yet (see evergreen + unresolved links below).
- These are your raw material. You are not trying to make them good - you are trying to
  make them *exist* so the review step has something to distill.

> [!note] In YOUR vault
> The [[Fractal Note]] template (`99 - Templates/Fractal Note.md`) is exactly this note.
> To make the hotkey: Settings -> Core plugins -> enable **Unique note creator**, set the
> format to `YYYY-MM-DD HHmm` and (optionally) point it at a folder; then bind a hotkey in
> Settings -> Hotkeys ("Unique note creator: Create new unique note"). If you use Templater,
> set its "folder template" so new unique notes start from the Fractal Note template.

---

## 4. The random note revisit

The **maintenance / rediscovery** step, done every few months:

- Obsidian has a core **Random note** command (bind a hotkey). It jumps you to a random
  note in the vault.
- Steph uses it to **wander** his own vault, and opens the **local graph** at shallow depth
  (1 hop) to see what a note connects to.
- Purpose:
  1. **Rediscover** old ideas you forgot you had.
  2. **Create missing links** - connect a note you land on to newer ones.
  3. **Maintenance** - fix formatting to match your latest style-guide rules.
- He deliberately does **not** automate this with AI: *"Don't delegate understanding."* The
  point is that *you* re-read and re-connect, which is how patterns in your own thinking
  become visible.

> [!tip] In YOUR vault
> Settings -> Core plugins -> enable **Random note**, then Settings -> Hotkeys -> bind
> "Open random note". Open the local graph from the note's ... menu or the right sidebar.

---

## 5. Evergreen notes

An **evergreen note** is a note about a single idea, written in your own words, that you
**keep and improve over time** - as opposed to a dated log entry you never touch again.

- Term popularized by **Andy Matuschak**; Steph links his own essay
  *"Evergreen notes turn ideas into objects that you can manipulate."*
- Properties of a good evergreen note:
  - **Atomic** - one concept per note (so it can be linked and reused precisely).
  - **Concept-oriented** - titled by the *idea*, not the date or source
    (e.g. `Constants cannot be reassigned`, not `Notes from chapter 4`).
  - **Densely linked** - it points to and is pointed to by related notes.
  - **Written for your future self** - full sentences, not cryptic fragments.
- Where they come from: the **best** thoughts that survive the fractal review get rewritten
  as evergreen notes. A fleeting `2026-09-15 1503` capture might graduate into a permanent,
  well-titled evergreen note.
- **Unresolved links feed this.** When you type `[[Some idea]]` before that note exists, you
  have left a breadcrumb. Later, when the idea has earned it, you click the link and write
  the evergreen note. The graph literally shows you which evergreen notes are "wanted."

> [!note] In YOUR vault
> Your Terraform notes are already evergreen notes - atomic (one concept each), concept-titled
> (`Root Module`, `Terraform Value Types`), and cross-linked under a MOC. `40 - Notes` is your
> evergreen home. Keep writing there in that same style.

---

## 6. Bases (viewing notes by `categories`)

**Bases** is Obsidian's built-in database-style view (a core feature in current Obsidian).
It is how Steph replaces folders with the **`categories` property**.

- A **Base** is a saved view that reads the **properties** (YAML frontmatter) of your notes
  and shows them as a **table or cards** - like a spreadsheet or Notion database, but built
  live from your plain Markdown files. Nothing is duplicated; the files stay the source of truth.
- You give it a **filter** (e.g. `categories contains books`) and choose **columns** (e.g.
  `author`, `genres`, `rating`, `end`). Every note that matches shows up as a row automatically.
- This is why his **property rules** matter: because `genres` is the *same property* on books,
  movies, and shows, one Base filtered to `genres contains sci-fi` shows all your sci-fi across
  every medium in one place. Folders can't do that; a property-driven view can.
- A "Category" note (e.g. `Books`) is really just a note that embeds a Base showing everything
  in that category - an auto-updating index page.

> [!info] Bases vs Dataview (what YOU have)
> **Dataview** (already installed in your vault) does the same job with a code query. Your
> dashboards already do this - e.g. Home's "Currently reading / watching" is a Dataview table
> filtered by `status`. Think of it as:
> - **Bases** = point-and-click, stored as a `.base` view, official/core.
> - **Dataview** = write a query in a code block (```` ```dataview ````), community plugin, more
>   powerful/flexible.
>
> You can use either. Your `Reading Dashboard`, `Film Dashboard`, and `Home` are Dataview
> "Bases" already. If you enable the Bases feature you can rebuild those as click-to-configure
> tables.

**Minimal Dataview example** (the manual version of a Base) - all sci-fi across books and films,
sorted by your rating:

```dataview
TABLE genres, rating, end AS "finished"
FROM "20 - Literature" OR "30 - Film"
WHERE contains(genres, "sci-fi")
SORT rating DESC
```

---

## Connections
- [[Steph Ango Vault System (MOC)]]
- [[Obsidian Cheat Sheet (MOC)]]
- [[Fractal Note]]
- [[Weekly Review]]
- [[Reference]]

## Sources
- Steph Ango, "My vault" - https://stephango.com/vault
- Steph Ango, "Evergreen notes turn ideas into objects..." - https://stephango.com/evergreen-notes
- Andy Matuschak, "Evergreen notes" - https://notes.andymatuschak.org/Evergreen_notes
- Obsidian Help, "Bases" - https://help.obsidian.md/bases
- Obsidian Help, "Unique note creator" - https://help.obsidian.md/plugins/unique-note
- Obsidian Help, "Random note" - https://help.obsidian.md/plugins/random-note
- Obsidian Help, "Backlinks" - https://help.obsidian.md/plugins/backlinks
