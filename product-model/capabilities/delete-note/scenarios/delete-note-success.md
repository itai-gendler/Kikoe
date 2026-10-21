---
kind: primary
routes:
  desktop: Desktop
steps:
- text: Confirm deletion of the note.
  kind: actor
  entities:
  - entity: note
    effect: reads
    facts: []
  contexts:
    desktop:
      place: desktop::note
  actor: user
- text: Remove the note, its recording text and original audio, and its speaker identities.
  kind: product
  entities:
  - entity: note
    effect: removes
  - entity: recording
    effect: removes
    from: Ready
    with: note
  - entity: speaker
    effect: removes
    with: note
  contexts:
    desktop:
      place: desktop::note
  actor: user
references:
- kind: code
  role: implementation
  target: src/kikoe/ui/note_actions.py#NoteActions._delete
- kind: code
  role: implementation
  target: src/kikoe/storage/library.py#Library.delete_note
---

# Delete note

## Trigger

The user chooses Delete Note and confirms.

## Outcome

The note, every recording in it with its text and original audio, and its speakers are deleted.

## Edge cases

- Cancelling confirmation preserves everything.
- Pending and incomplete recordings are removed with the note as well.
