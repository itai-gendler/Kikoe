---
kind: alternate
routes:
  desktop: Desktop
steps:
- text: Choose Keep as New Speaker for a matched label.
  kind: actor
  entities:
  - entity: speaker
    effect: reads
    facts: []
  contexts:
    desktop:
      place: desktop::note
  actor: user
- text: Restore the recording label’s original speaker assignment and confirm it.
  kind: product
  entities:
  - entity: recording
    effect: changes
    facts:
    - Speaker assignments
  - entity: speaker
    effect: reads
    facts: []
  contexts:
    desktop:
      place: desktop::note
  actor: user
references:
- kind: code
  role: implementation
  target: src/kikoe/ui/speaker_dialog.py
- kind: code
  role: implementation
  target: src/kikoe/core/speakers.py
- kind: code
  role: implementation
  target: src/kikoe/storage/library.py#Library.match_speakers
---

# Separate a previously matched label

## Trigger

The user revisits matching for a recording.

## Outcome

Keep as New Speaker restores that label’s original independent identity.
