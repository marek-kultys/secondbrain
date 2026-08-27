
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
source_url:  # direct URL to the online version; extract from PDF footer/metadata when available; omit if no online version exists
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
source: <publication or site name>
source_url: https://...
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
- Raw information lives in `raw/`; processed knowledge in `wiki/`. Use `wiki/` to retrieve information when asked about anything.
- `index.md` is a flat catalogue of all `wiki/` notes, grouped by folder, with a total count and last-updated date. Entries are plain text titles — no wiki links. Update when `brain routine` runs.
- Log every significant vault operation (structural change, new knowledge, update to key documents) in `log.md` using `patterns/log_entry.md`. Timestamps must be `YYYY-MM-DD HH:MM:SS` — fetch current time with `date '+%H:%M:%S'` before writing. Prepend new entries (newest at top).
- **Log compression:** everything stays in the single `log.md` file — no separate archive files. Full entries (using `patterns/log_entry.md`) live at the top for the current quarter. When a `brain routine` run is the first one to touch `log.md` in a new quarter, compress all entries from the quarter that just ended into one-line summaries (`- **<header>** — <one-sentence gist>`) under the "Compressed history" heading at the end of the file, oldest entries last. Compressed entries are never restored to full detail; git history retains the originals if ever needed.
- New facts in `facts.md` are also prepended.
- All wiki notes must follow `patterns/note.md`: frontmatter (title/author/source/source_url/year_published/tags/raw/type/read_status) and five body sections (Core idea, Key principles, Connections, Timeline & context, My notes). Include `source_url:` only when an online version exists; omit the field otherwise.
- The controlled vocabulary for `type` lives only in `patterns/note.md` — never repeat it in wiki notes.
- `log.md` and `facts.md` must contain no `[[wikilinks]]`. Wiki notes must not link to `patterns/` files.
- Always read the relevant template before creating a new document of that type.


## Brain routine (organise, clean up, track new knowledge)
On every `brain routine` command, do this:

1. **Detect unprocessed items:** Recursively scan all of `raw/` — no directory name (e.g. `unfinished/`) is a reason to skip. A file is covered only if (a) a matching wiki note exists AND (b) that note's `raw:` frontmatter path resolves to the file on disk. Title match alone is not sufficient.
2. **Process URLs:** Read `raw/URLs/urls.md`, collect all `[ ]` entries. Fetch each with WebFetch; flag and skip unreachable ones. Ask which have been read (sets `read_status`). Create one wiki note per URL; set `source:` to the URL and `raw: "[[raw/URLs/urls.md]]"`. Place in the most appropriate `wiki/` subfolder. Mark `[x]` and append `→ [[Note Title]]` in place.
3. **Process new items:** Create a wiki note for each unprocessed file. For documents not created by me, ask if I read them first. For PDFs, try `pdftotext <file> - | grep -oE 'https?://[^ )},]+' | head -1` for a source URL; for Distill papers look for the `note = {https://distill.pub/...}` BibTeX block. Set `source_url:` only if a clean canonical URL is found; omit it otherwise.
4. **Update `persona/`:** If any new `raw/about-me/` items were processed, update the relevant `persona/` documents.
5. **Validate raw paths — exhaustively:** Verify every wiki note's `raw:` paths exist on disk — check all notes, not just recent ones. Fix and report every broken path (common cause: directory renames).
6. **Check MOC currency:** Verify all notes in each MOC folder are listed and counts are accurate. Update where needed.
7. **Audit note quality:** Flag stubs (Core idea or Key principles empty or placeholder) and notes missing required frontmatter fields or any body section. Report all — do not auto-fill.
8. **Update `index.md`:** Ensure count matches actual total, all folders and notes are listed, no wiki links present.
9. **Update `log.md` and print summary:** Prepend a log entry capturing what changed. Compress log entries older than 4 months. Print a short summary.


## URL routine (process online articles)
On `process urls` command:
1. Read `raw/URLs/urls.md`, collect all `[ ]` entries. If none, report and stop.
2. Fetch each URL with WebFetch. Flag and skip unreachable or paywalled ones.
3. Ask which have been read before creating notes — batch the question across all queued URLs.
4. Create one wiki note per URL following `patterns/note.md`. Set `source:` to the URL and `raw: "[[raw/URLs/urls.md]]"`. Place in the most appropriate `wiki/` subfolder (root for standalone articles; existing subfolders for collection content).
5. Mark each entry `[x]` and append `→ [[Note Title]]` in place — do not move lines.
6. Update `index.md` and prepend an entry to `log.md`.


## Generating a curious fact
On every  `give me a fact` or `get me a fact` or `get a new fact` command:
1. Search `wiki/` and `raw/` and generate a new fact
2. New fact must be an inference grounded in the vault; it must span at least 3 separate knowledge sources
3. Summarise the fact in a few sentences and quote the sources (with page numbers)
4. Prepend the new fact to `facts.md` following `patterns/facts.md`