---
tags: [moc, topic/obsidian, topic/pkm, reference]
created: 2026-09-15
source: https://stephango.com/vault
---

# Steph Ango Vault System (MOC)

> [!summary]
> Steph Ango is the CEO of Obsidian. His public vault (stephango.com/vault) is a
> masterclass in a **low-friction, link-first, property-driven** note system built
> on the idea that your notes are just **files you own** ("file over app"). This note
> explains his system in plain language and shows how it has been adapted to *your*
> existing vault - keeping your numbered folders and dashboards, while adopting his
> conventions, ratings, and composable templates. Obsidian Sync is intentionally ignored;
> you already back up with Obsidian Git.

Companion note: [[Obsidian Cheat Sheet (MOC)]] (shortcuts, syntax, plugins).

---

## 1. The core idea: file over app

Everything rests on one belief: **if you want digital notes that last, they must be
plain files you control, in open formats.** Obsidian is just a nice window onto a folder
of Markdown files. No lock-in, no database. This is why the whole system is deliberately
simple - plain `.md` text, standard Markdown, and metadata stored as plain YAML at the
top of each file.

> [!tip] Takeaway
> Don't over-engineer. Favor plain text, standard Markdown, and conventions you can keep
> for years over clever automation you'll abandon.

---

## 2. His personal rules (his "style guide")

Steph writes down a short style guide so that hundreds of tiny future decisions collapse
into one. His rules, verbatim in spirit:

- Avoid splitting content into multiple vaults.
- Avoid folders for organization.
- Avoid non-standard Markdown.
- Always **pluralize** categories and tags (`books`, `genres`, not `book`, `genre`).
- Use internal links **profusely**.
- Use **YYYY-MM-DD** dates everywhere.
- Use the **7-point scale** for ratings.
- Keep a **single to-do list per week**.

> [!quote] Why rules help
> "Having a consistent style collapses hundreds of future decisions into one, and gives me
> focus... Choose rules that feel comfortable to you and write them down. You can always
> change your rules later."

**Your adapted rule set** (see [[#8 Your style guide]] at the bottom - edit it freely).

---

## 3. Folders vs. the `categories` property

This is his most distinctive choice. Steph uses **very few folders** because many notes
belong to more than one area of thought, and deciding "where does this go?" is friction.

- Most notes live in the **root** of the vault - his personal writing (journal, essays,
  evergreen notes). "If a note is in the root, I know it's something I wrote."
- He navigates by **Quick Switcher, backlinks, and links inside notes** - almost never the
  file tree.
- Notes are organized by a **`categories` property**, not by folder. A "Category" note
  (e.g. `Books`) shows an overview of everything in that category using the **Bases** plugin.

He keeps only a handful of folders:

| Folder | Purpose |
|---|---|
| `References` | Things outside his world: books, movies, places, people, podcasts. Named by title, e.g. `Perfect Days.md`. |
| `Clippings` | Things **other people** wrote (essays, articles), saved with Web Clipper. |
| `Attachments` | Images, audio, video, PDFs (hidden from navigation). |
| `Daily` | Daily notes named `YYYY-MM-DD.md`. He writes nothing in them - they exist only to be **linked to**. |
| `Templates` | Templates. |

> [!note] How this maps to YOUR vault
> You already have a working **numbered-folder** vault (`10 - Work`, `20 - Literature`,
> `30 - Film`, `40 - Notes`, `50 - People`...) with Dataview dashboards. **We are keeping it.**
> Think of your folders as Steph's "References" split by kind. You get his *conventions*
> (categories property, ratings, heavy linking, composable templates) layered on top -
> without throwing away your dashboards. Adopt the `categories` property as an *additional*
> way to slice notes across folders (e.g. a `sci-fi` genre that spans books + films).

---

## 4. Links: the real organizing system

Folders barely matter because **links do the organizing**. Steph's habits:

- **Link the first mention** of anything - a person, place, movie, idea.
- Write journal entries as a stream of consciousness, linking as you go:
  > I went to see the movie [[Perfect Days]] with [[Aisha]] at [[Vidiots]] and had Filipino
  > food at [[Little Ongpin]]. I loved this quote: [[Next time is next time, now is now]].
- **Unresolved links are a feature.** Linking `[[Aisha]]` before that note exists leaves a
  breadcrumb; the note can be filled in later. These become future connections.
- Over time this lets you trace **how ideas emerged** and branched.

> [!tip] Practical habit
> Don't stop to create a note when you link it. Just type `[[Thing]]`. Click it later when
> you actually have something to say. The graph fills itself in.

---

## 5. Fractal journaling + random revisit

How Steph keeps a growing knowledge base from turning into chaos:

1. **Capture** - Throughout the day, the *unique note* hotkey creates a note prefixed
   `YYYY-MM-DD HHmm` for each individual thought. (Template: [[Fractal Note]].)
2. **Compile** - Every few days he reviews those fragments and pulls out the salient ones.
3. **Zoom out** - Those reviews are reviewed monthly; monthly reviews are reviewed yearly.
   The result is a **fractal web** he can zoom in and out of. (Template: [[Weekly Review]].)
4. **Random revisit** - Every few months he uses the **Random note** hotkey to wander the
   vault, viewing the **local graph** at shallow depth to rediscover and re-link old ideas,
   and to fix formatting under new rules.

> [!quote]
> "Don't delegate understanding." He deliberately does *not* automate this with AI - the
> manual review is how he understands his own patterns.

---

## 6. Properties and templates (the "advanced templating")

Almost every note starts from a **template**, with **properties** (YAML) at the top so the
note is easy to find later. This is the part you asked about.

**His property groups:**

| Group | Example properties |
|---|---|
| Dates | `created`, `start`, `end`, `published` |
| People | `author`, `director`, `artist`, `cast`, `host`, `guests` |
| Themes | `genre`, `type`, `topic`, related notes |
| Locations | `neighborhood`, `city`, `coordinates` |
| Ratings | `rating` (see below) |

**His four property rules:**

1. **Reusable across categories.** Use the *same* property name everywhere so you can query
   across kinds - e.g. `genres` is shared by books, movies, and shows, so you can pull an
   archive of all `sci-fi` in one place.
2. **Composable templates.** `Person` and `Author` are *separate* templates that can both be
   added to the same note. Small, mix-and-match building blocks - not one giant template.
3. **Short property names** are faster to type - `start` instead of `start-date`.
4. **Default to list-type properties** (`[]`) whenever a field might hold more than one value
   in future (e.g. `genres`, `cast`).

> [!info] Bases and property types
> Obsidian stores which property is a `date` / `number` / `text` / `list` in
> `.obsidian/types.json`. The **Bases** plugin then renders a "category" as a live table/board
> of every note sharing a property. If you don't have Bases, your **Dataview** dashboards do
> the same job (your Home/Reading/Film dashboards already query by `type` and `status`).

Templates created for you (in `99 - Templates/`):

- [[Reference]] - the flagship: all property groups, for any "thing outside your world".
- [[Person]] - composable people block (contacts, authors, directors...).
- [[Place]] - composable location block (neighborhood, city, coordinates).
- [[Fractal Note]] - the `YYYY-MM-DD HHmm` quick-thought capture note.
- [[Weekly Review]] - the fractal journaling weekly compile + single weekly to-do list.

(Your existing [[99 - Templates/Book|Book]] and [[99 - Templates/Film|Film]] templates still
work; Section 7 shows the optional 7-point upgrade.)

---

## 7. The 7-point rating scale

Steph rates **anything** with an integer from **1 to 7** (verbatim):

| Rating | Meaning |
|---|---|
| **7 - Perfect** | Must try, life-changing, go out of your way to seek this out |
| **6 - Excellent** | Worth repeating |
| **5 - Good** | Don't go out of your way, but enjoyable |
| **4 - Passable** | Works in a pinch |
| **3 - Bad** | Don't do this if you can |
| **2 - Atrocious** | Actively avoid, repulsive |
| **1 - Evil** | Life-changing in a bad way |

> [!quote] Why 7?
> "I need more granularity at the top, for the good experiences, and 10 is too granular."

> [!warning] Heads up for your dashboards
> Your current `Book`/`Film` templates use `rating: 1-5`. If you switch to 1-7, just keep it
> consistent going forward - your Dataview dashboards sort/show the number either way. The new
> [[Reference]] template already uses the 1-7 scale.

---

## 8. Your style guide

> [!example] Edit this to make it yours
> - One vault (this one). Back up with Obsidian Git (already running every 10 min).
> - Keep the numbered folders, but let `categories`/`genres` cross-cut them.
> - Pluralize tags and categories: `books`, `genres`, `people`.
> - `YYYY-MM-DD` dates everywhere. Quick-thoughts as `YYYY-MM-DD HHmm`.
> - Link the first mention of everything; leave unresolved links as breadcrumbs.
> - Ratings on the 1-7 scale.
> - One to-do list per week (in the [[Weekly Review]]).
> - Every few months: Random note revisit + fix formatting.

---

## Connections
- [[Obsidian Cheat Sheet (MOC)]]
- [[Reference]]
- [[Person]]
- [[Place]]
- [[Fractal Note]]
- [[Weekly Review]]

## Sources
- Steph Ango, "My vault" - https://stephango.com/vault
- Steph Ango, "File over app" - https://stephango.com/file-over-app
- Steph Ango, vault repo - https://github.com/kepano/kepano-obsidian
- Obsidian Help, "Properties" - https://help.obsidian.md/Editing+and+formatting/Properties
- Obsidian Help, "Bases" - https://help.obsidian.md/bases
