---
kind: alternate
routes:
  desktop: Desktop
steps:
- text: Export original recording audio.
  kind: actor
  entities:
  - entity: recording
    effect: reads
    facts:
    - Original audio
  contexts:
    desktop:
      place: desktop::note
  actor: user
- text: Choose a destination.
  kind: actor
  entities: []
  contexts:
    desktop:
      place: desktop::note
  actor: user
- text: Copy the retained recording audio with its original extension.
  kind: product
  entities:
  - entity: recording
    effect: reads
    facts:
    - Original audio
  - entity: note
    effect: reads
    facts:
    - Title
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

# Export retained original audio

## Trigger

The user chooses Export Original Audio for a recording.

## Outcome

The retained audio is copied unchanged to the chosen destination.

## Edge cases

- Missing original audio is explained.
- Changing transcription upload format never changes the original audio exported here.
