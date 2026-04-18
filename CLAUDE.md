## Setting up new brain
On `set up new brain` command, create the following directory structure with files in the root directory where this file lives:
```
/patterns
/patterns/log_entry.md
/patterns/note.md
/persona
/raw
/wiki
checklist.md
index.md
log.md
```

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
1. Search through the stored knowledge and generate a new fact
2. New fact must be an inference that spans at least 3 separate knowledge sources
3. Summarise the fact in a few sentences and quote the sources (with page numbers)