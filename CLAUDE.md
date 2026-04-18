## Setting up new brain

#### 1. Build structure
On `set up new brain` command, create the following directory structure with files in the root directory where this file lives:
```
/patterns
/patterns/facts.md
/patterns/log_entry.md
/patterns/note.md
/persona
/raw
/wiki
checklist.md
facts.md
index.md
log.md
```
#### 2. Populate templates
Populate `.md` documents in `patterns` directory with the following template specification:

**`patterns/note.md`**
```
---
name: Note Template
description: Template for all wiki notes — one note per processed item from /raw
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
description: Template for entries in /log.md — one entry per significant vault operation
type: template
---

## YYYY-MM-DD HH:MM:SS — <Action Title>

**Type:** process | edit | create | delete | restructure | other  
**Scope:** <folder or files affected>

<1–3 sentences: what changed and why>

---
```

**`patterns/facts.md`**
```
---
name: Fact Template
description: Template for entries in /facts.md — one entry per generated fact
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
Do this only once.


## Admin rules
- This Obsisian vault is my digital brain. I store raw information in `/raw` and you index and manage it in `/wiki`. Use `/wiki` to retrieve information when asked about anything.
- Every significant vault operation (structural change, new knowledge, update to key documents) must be logged in `/log.md` using the `patterns/log_entry.md` template.
- Log entries must include a full timestamp: `YYYY-MM-DD HH:MM:SS` — retrieve the current time via `date '+%H:%M:%S'` before writing each entry.
- Log entries are prepended (newest at top).
- All wiki notes must conform to `patterns/note.md`: meta frontmatter (name, description, type: template is for templates; notes use title/author/source/year_published/tags/raw/type) and five body sections (Core idea, Key principles, Connections, Timeline & context, My notes).
- The controlled vocabulary for `type` lives only in `patterns/note.md` — never repeat it in individual wiki notes.


## Templates
- For wiki notes: follow `patterns/note.md`
- For log entries: follow `patterns/log_entry.md`
- Always read the relevant template before creating a new document of that type


## Brain routine (organise, clean up, track new knowledge)
On every `brain routine` command, do this:
1. Check if there are any new items in `/raw` that have not been processed into `/wiki`
2. Process new items from `/raw` into `/wiki` using templates for notes and other documents described in `/patterns` (when you process document not created by me, always ask if I read them)
3. Clean up the brain, checking if links are complete, if there are any unaccounted for documents, and if all `/wiki` adhere to relevant patterns — update where needed 
4. Once done, update `/log.md` to capture what changed
5. In terminal, print a short message summarising what has been done


## Generating a curious fact
On every `get me a fact` command:
1. Search through the stored knowledge in `/raw` and `/wiki` and generate a new fact
2. New fact must be an inference grounded in the vault; it must span at least 3 separate knowledge sources
3. Summarise the fact in a few sentences and quote the sources (with page numbers)
4. Prepend the new fact to `/facts.md` following `patterns/facts.md`