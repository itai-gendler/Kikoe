---
kind: alternate
routes:
  desktop: Desktop
steps:
- text: Enter new recording timestamps.
  kind: actor
  entities:
  - entity: recording
    effect: reads
    facts:
    - Timestamps
  contexts:
    desktop:
      place: desktop::note
  actor: user
- text: Save the recording timestamps and remember their previous values for Undo.
  kind: product
  entities:
  - entity: recording
    effect: changes
    facts:
    - Timestamps
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

# Add, change or clear passage times

## Trigger

The user edits start or end time.

## Outcome

Valid changes are saved; either timestamp may be cleared.
