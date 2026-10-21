---
kind: validation
routes:
  desktop: Desktop
steps:
- text: Enter a title.
  kind: actor
  entities: []
  contexts:
    desktop:
      place: desktop::notes
  actor: user
- text: The title is blank or the local save fails.
  kind: condition
  entities: []
  contexts:
    desktop:
      place: desktop::notes
- text: Keep the creation form and report the save error when applicable.
  kind: product
  entities: []
  contexts:
    desktop:
      place: desktop::notes
  actor: user
references:
- kind: code
  role: implementation
  target: src/kikoe/ui/new_note_dialog.py
- kind: code
  role: implementation
  target: src/kikoe/ui/note_actions.py#NoteActions._create_note
---

# Keep a title available after failed creation

## Trigger

The title is blank or saving fails.

## Outcome

No successful creation is shown; a save failure retains entered text for retry.
