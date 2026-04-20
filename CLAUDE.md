
# Instructions for Claude Code
## Setting up new brain
Do this only once when setting up the vault. Do not set up a new brain if there is a `raw/` or `wiki/` directory.

#### 1. Build structure
On `set up new brain` command, create the following directory structure with files in the root directory where this file lives:
```
patterns/
patterns/facts.md
patterns/log_entry.md
patterns/note.md
patterns/url_entry.md
persona/
raw/
wiki/
checklist.md
facts.md
index.md
log.md
raw/URLs/
raw/URLs/urls.md
```
Delete `Welcome.md` if it exists in the root directory (Obsidian creates this file automatically).

#### 2. Populate templates
Populate `.md` documents in `patterns` directory with the following template specification:

**`patterns/note.md`**
```
---
name: Note Template
description: Template for all wiki notes — one note per processed item from raw/
type: template
---

## Frontmatter

\```yaml
---
title:
author:
source:
year_published:
tags: []
raw:
type:  # academic-paper | opinion-piece | thought-leadership | my-writing | book | talk | article | interview | other
read_status:  # read | unread
---
\```

## Core idea
*One or two sentences capturing the central argument or insight.*

## Key principles
- 

## Connections
- 

## Timeline & context
**Year discovered:** 
**Related projects:** 
*Note any ideas here that conflict with, build on, or evolved from other notes in the vault. Use this to layer the development of an idea over time.*

## My notes
*Your own reactions, disagreements, applications, and open questions.*
```

**`patterns/log_entry.md`**
```
---
name: Log Entry Template
description: Template for entries in log.md — one entry per significant vault operation
type: template
---

## YYYY-MM-DD HH:MM:SS — <Action Title>

**Type:** process | edit | create | delete | restructure | other  
**Scope:** <folder or files affected>

<1–3 sentences: what changed and why>

---
```

**`patterns/url_entry.md`**
```
---
name: URL Entry Template
description: Template for entries in raw/URLs/urls.md — one entry per online article queued for processing
type: template
---

## Format

\```
- [ ] https://... — optional short label
- [x] https://... — optional short label → [[Wiki Note Title]]
\```

## Rules
- `[ ]` = queued, not yet processed into a wiki note
- `[x]` = processed; append `→ [[Wiki Note Title]]` to link back to the created note
- The short label is optional but recommended when the URL is not self-explanatory
- `[x]` entries are marked in place — no sections, no moving lines

## Wiki note for a URL-sourced article

\```yaml
---
title:
author:
source: https://...
year_published:
tags: []
raw: "[[raw/URLs/urls.md]]"
type:
read_status:
---
\```
```

**`patterns/facts.md`**
```
---
name: Fact Template
description: Template for entries in facts.md — one entry per generated fact
type: template
---

## YYYY-MM-DD — <Fact title: a short declarative statement>

<2–4 sentences stating the fact as an inference. Bold the key claim. Each sentence should add something — no padding.>

**Sources:**
- *<Title>*, <Author>, <Publication>, <Year>, <page or section reference>
- *<Title>*, <Author>, <Publication>, <Year>, <page or section reference>
- *<Title>*, <Author>, <Publication>, <Year>, <page or section reference>

---
```
#### 3. Finish

Once done, log this as first action in `log.md` adhering to brain rules and template patterns.


## Admin rules
- This Obsisian vault is my digital brain. I store raw information in `raw/` and you index and manage it in `wiki/`. Use `wiki/` to retrieve information when asked about anything.
- `index.md` is a flat catalogue of all notes in `wiki/`, grouped by folder, with a total count and last-updated date in the header. Follow `patterns/index.md`. List entries as plain text titles — no wiki links. Update `index.md` when `brain routine` is run.
- Every significant vault operation (structural change, new knowledge, update to key documents) must be logged in `log.md` using the `patterns/log_entry.md` template.
- Log entries must include a full timestamp: `YYYY-MM-DD HH:MM:SS` — retrieve the current time via `date '+%H:%M:%S'` before writing each entry.
- New log entries in `log.md` and new facts in `facts.md` are prepended (newest at top).
- All wiki notes must conform to `patterns/note.md`: meta frontmatter (name, description, type: template is for templates; notes use title/author/source/year_published/tags/raw/type) and five body sections (Core idea, Key principles, Connections, Timeline & context, My notes).
- The controlled vocabulary for `type` lives only in `patterns/note.md` — never repeat it in individual wiki notes.
- `log.md` and `facts.md` must contain no `[[wikilinks]]` of any kind — no links to wiki notes, no links to patterns/ templates.
- Wiki notes must not link to `patterns/` templates (e.g. do not write `[[patterns/note.md]]` or `[[patterns/log_entry]]` inside a wiki note).


## Templates
- For wiki notes: follow `patterns/note.md`
- For log entries: follow `patterns/log_entry.md`
- For index: follow `patterns/index.md`
- Always read the relevant template before creating a new document of that type


## Brain routine (organise, clean up, track new knowledge)
On every `brain routine` command, do this:

1. **Detect unprocessed items:** Recursively scan all files in `raw/` including all subdirectories at any depth. Do not skip subdirectories by name (e.g. `unfinished/` is not a reason to skip). A raw file is only considered covered if (a) a wiki note exists with a matching title AND (b) that note's `raw:` frontmatter path resolves to the file on disk. A title match alone is not sufficient.
2. **Process URLs:** Read `raw/URLs/urls.md` and collect all unchecked `[ ]` entries. For each URL, fetch content using WebFetch. If a URL is unreachable, flag and skip. Ask which URLs have been read before creating notes (read_status depends on the answer). Create one wiki note per URL following `patterns/note.md`; set `source:` to the URL and `raw: "[[raw/URLs/urls.md]]"`. Place notes in the most appropriate `wiki/` subfolder. Mark each entry as `[x]` and append `→ [[Note Title]]` in place — do not move lines.
3. **Process new items:** For each unprocessed raw file, create a wiki note following `patterns/note.md`. When processing a document not created by me, always ask if I read it first.
4. **Update `persona/`:** If any new `raw/about-me/` items were processed, update the relevant `persona/` documents to reflect the new information.
5. **Validate raw paths — exhaustively:** For every wiki note (not just recently edited ones), verify each path in the `raw:` frontmatter exists on disk. Do not spot-check; check all notes. Fix broken paths and report every one found — common cause is directory renames (e.g. `conferences/` → `presentations/`).
6. **Check MOC currency:** For each MOC document, verify all notes in its folder are listed and the note count is accurate. Update where needed.
7. **Audit note quality:** Flag notes where Core idea or Key principles are empty or contain only placeholder text (stubs), and notes missing required frontmatter fields or any of the five body sections. Report all issues — do not auto-fill.
8. **Update `index.md`:** Ensure count matches actual wiki note total, all folders and notes are listed, and no wiki links are present.
9. **Update `log.md` and print summary:** Prepend a log entry capturing what changed. Print a short summary in terminal.


## URL routine (process online articles)
On `process urls` command:
1. Read `raw/URLs/urls.md` and collect all unchecked `[ ]` entries. If none, report and stop.
2. For each URL, fetch content using WebFetch. Flag and skip any that are unreachable or paywalled.
3. Ask which URLs have been read before creating notes — can batch the question across all queued URLs.
4. Create one wiki note per URL following `patterns/note.md`. Set `source:` to the URL; set `raw: "[[raw/URLs/urls.md]]"`. Place notes in the most appropriate `wiki/` subfolder (root for standalone articles and books; existing subfolders for content that clearly belongs to a collection).
5. Mark each entry as `[x]` and append `→ [[Note Title]]` in place — do not move lines.
6. Update `index.md` and prepend an entry to `log.md`.


## Generating a curious fact
On every  `give me a fact` or `get me a fact` or `get a new fact` command:
1. Search through the stored knowledge in `index.md`, `wiki/` and `raw/` and generate a new fact
2. New fact must be an inference grounded in the vault; it must span at least 3 separate knowledge sources
3. Summarise the fact in a few sentences and quote the sources (with page numbers)
4. Prepend the new fact to `facts.md` following `patterns/facts.md`