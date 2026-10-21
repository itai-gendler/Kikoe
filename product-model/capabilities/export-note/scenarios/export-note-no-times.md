---
kind: validation
routes:
  desktop: Desktop
steps:
- text: Open export for the note.
  kind: actor
  entities:
  - entity: note
    effect: reads
    facts:
    - Title
  contexts:
    desktop:
      place: desktop::note
  actor: user
- text: No recording passage has timestamp information.
  kind: condition
  entities:
  - entity: recording
    effect: reads
    facts:
    - Timestamps
  contexts:
    desktop:
      place: desktop::note
- text: Explain why subtitle formats are unavailable.
  kind: product
  entities: []
  contexts:
    desktop:
      place: desktop::note
  actor: user
references:
- kind: code
  role: implementation
  target: src/kikoe/ui/export_controller.py
- kind: code
  role: implementation
  target: src/kikoe/ui/export_dialog.py
- kind: code
  role: implementation
  target: src/kikoe/core/export.py
---

# Explain unavailable subtitle formats

## Trigger

The note has no timestamp information.

## Outcome

Text and Markdown remain available; subtitle formats are unavailable.
