---
kind: primary
routes:
  desktop: Desktop
steps:
- text: Undo the latest saved passage edit.
  kind: actor
  entities: []
  contexts:
    desktop:
      place: desktop::note
  actor: user
- text: Restore recording text or timestamps to the preceding edit value.
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

# Undo the latest edit

## Trigger

The user chooses Undo in a note with saved passage edits.

## Outcome

The affected passage returns to its earlier text or times, which are saved, and the step can be redone.

## Edge cases

- History is limited to the open note and is cleared on switching notes or incompatible transcript replacement.
- A new edit clears the redo history.
- Successive text-only edits to the same passage within two seconds form one step until focus leaves or history is traversed.
