---
kind: primary
routes:
  desktop: Desktop
steps:
- text: Submit a changed nonempty note title.
  kind: actor
  entities:
  - entity: note
    effect: reads
    facts: []
  contexts:
    desktop:
      place: desktop::note
  actor: user
- text: Save the trimmed note title.
  kind: product
  entities:
  - entity: note
    effect: changes
    facts:
    - Title
  contexts:
    desktop:
      place: desktop::note
  actor: user
references:
- kind: code
  role: implementation
  target: src/kikoe/ui/note_actions.py#NoteActions._rename
- kind: code
  role: implementation
  target: src/kikoe/storage/notes.py#NoteRepository.rename_note
---

# Rename note

## Trigger

The user renames the open note, or a note from its row in the list, with a nonblank title.

## Outcome

The trimmed title is saved and shown in the list and the header.

## Edge cases

- Blank names cannot be submitted. An unchanged name leaves the note alone.
