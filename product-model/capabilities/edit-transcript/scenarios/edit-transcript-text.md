---
kind: primary
routes:
  desktop: Desktop
steps:
- text: Edit recording transcript text.
  kind: actor
  entities:
  - entity: recording
    effect: reads
    facts:
    - Transcript
  contexts:
    desktop:
      place: desktop::note
  actor: user
- text: Save the edited recording passage and remember the edit for Undo.
  kind: product
  entities:
  - entity: recording
    effect: changes
    facts:
    - Transcript
  contexts:
    desktop:
      place: desktop::note
  actor: user
references:
- kind: code
  role: implementation
  target: src/kikoe/ui/transcript_row.py
- kind: code
  role: implementation
  target: src/kikoe/ui/segment_editor.py
- kind: code
  role: implementation
  target: src/kikoe/services/editing.py
- kind: code
  role: implementation
  target: src/kikoe/core/validation.py
---

# Save passage text

## Trigger

The user edits a saved transcript passage.

## Outcome

Nonempty text is saved after a typing pause or when leaving the passage; surrounding passages remain intact.

## Edge cases

- Unsaved typing can be reverted before it is committed.
- Pending edits remain visible while other changes reload the note.
- Preview and live unfinished text are not editable.
