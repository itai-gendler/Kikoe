---
kind: primary
routes:
  desktop: Desktop
steps:
- text: Submit a nonempty speaker name.
  kind: actor
  entities:
  - entity: speaker
    effect: reads
    facts: []
  contexts:
    desktop:
      place: desktop::note
  actor: user
- text: Save the speaker name without changing source labels or speaker number.
  kind: product
  entities:
  - entity: speaker
    effect: changes
    facts:
    - Name
  contexts:
    desktop:
      place: desktop::note
  actor: user
references:
- kind: code
  role: implementation
  target: src/kikoe/ui/speaker_editor.py
- kind: code
  role: implementation
  target: src/kikoe/storage/library.py#Library.rename_speaker
---

# Rename speaker

## Trigger

The user opens Rename Speaker from a speaker name and saves a nonblank name.

## Outcome

Every passage linked to that speaker shows the new name; the speaker keeps its number.

## Edge cases

- Blank names cannot be saved.
- Unsaved form changes require a discard decision when dismissing; Cancel discards them.
