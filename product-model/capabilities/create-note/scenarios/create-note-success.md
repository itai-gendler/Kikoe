---
kind: primary
routes:
  desktop: Desktop
steps:
- text: Enter and submit a nonempty title.
  kind: actor
  entities: []
  contexts:
    desktop:
      place: desktop::notes
  actor: user
- text: Create the empty note with its trimmed title, creation time, zero duration and both display options
    on.
  kind: product
  entities:
  - entity: note
    effect: creates
    facts:
    - Title
    - Created
    - Recordings
    - Duration
    - Display options
  contexts:
    desktop:
      place: desktop::notes
  actor: user
- text: Open the new note.
  kind: product
  entities:
  - entity: note
    effect: reads
    facts:
    - Title
    - Created
    - Recordings
    - Duration
    - Display options
  contexts:
    desktop:
      place: desktop::note
  actor: user
references:
- kind: code
  role: implementation
  target: src/kikoe/ui/new_note_dialog.py
- kind: code
  role: implementation
  target: src/kikoe/ui/note_actions.py#NoteActions._create_note
---

# Create note

## Trigger

The user submits a title.

## Outcome

The empty note is selected and ready for audio.
