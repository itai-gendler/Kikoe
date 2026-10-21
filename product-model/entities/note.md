---
domain: notes
relations:
- entity: recording
  verb: contains
  cardinality: one-to-many
- entity: speaker
  verb: identifies
  cardinality: one-to-many
- entity: microphone-capture
  verb: receives
  cardinality: one-to-many
references:
- kind: code
  role: implementation
  target: src/kikoe/core/models.py#Note
- kind: code
  role: implementation
  target: src/kikoe/storage/library.py
---

# Note

A titled item in the local library, holding recordings in source order and note-wide speaker identities.

## Information kept

- **Title** — The chosen title, the imported file’s name, or the original title when recovery recreates the note.
- **Created** — When the note was created.
- **Recordings** — Ordered audio sections; an empty note has none.
- **Duration** — The sum of its recording durations.
- **Display options** — Whether timestamps and speaker names are shown and used by default for text output.
