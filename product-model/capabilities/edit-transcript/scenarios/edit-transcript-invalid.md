---
kind: validation
routes:
  desktop: Desktop
steps:
- text: Enter passage text or timing.
  kind: actor
  entities: []
  contexts:
    desktop:
      place: desktop::note
  actor: user
- text: The proposed values fail validation.
  kind: condition
  entities: []
  contexts:
    desktop:
      place: desktop::note
- text: Keep the saved recording text and timestamps.
  kind: product
  entities:
  - entity: recording
    effect: reads
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

# Reject blank text or invalid times

## Trigger

Edited text is blank, a timestamp is invalid, or an end is not later than its start.

## Outcome

The invalid edit is explained and saved content is retained.
