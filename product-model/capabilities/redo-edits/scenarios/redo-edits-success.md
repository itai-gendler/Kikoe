---
kind: primary
routes:
  desktop: Desktop
steps:
- text: Redo the last undone passage edit.
  kind: actor
  entities: []
  contexts:
    desktop:
      place: desktop::note
  actor: user
- text: Reapply recording text or timestamps from the undone edit.
  kind: product
  entities:
  - entity: recording
    effect: changes
    facts:
    - Transcript
    - Timestamps
  contexts:
    desktop:
      place: desktop::note
  actor: user
references:
- kind: code
  role: implementation
  target: src/kikoe/core/edit_history.py#EditHistory
- kind: code
  role: implementation
  target: src/kikoe/services/editing.py#EditingSession
---

# Redo an undone edit

## Trigger

The user chooses Redo after undoing an edit.

## Outcome

The passage takes the undone text or times again, and they are saved.

## Edge cases

- History is limited to the open note and is cleared on switching notes or incompatible transcript replacement.
- A new edit clears the redo history.
- Successive text-only edits to the same passage within two seconds form one step until focus leaves or history is traversed.
