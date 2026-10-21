---
kind: primary
routes:
  desktop: Desktop
steps:
- text: Stop the playing recording or sample.
  kind: actor
  entities:
  - entity: recording
    effect: reads
    facts: []
  contexts:
    desktop:
      place: desktop::note
  actor: user
- text: Release playback of the recording audio.
  kind: product
  entities:
  - entity: recording
    effect: reads
    facts:
    - Original audio
  contexts:
    desktop:
      place: desktop::note
  actor: user
references:
- kind: code
  role: implementation
  target: src/kikoe/services/playback.py#Playback.stop
- kind: code
  role: implementation
  target: src/kikoe/ui/speaker_controller.py
---

# Stop playback

## Trigger

The user stops the recording or sample that is playing.

## Outcome

Playback ends; choosing the same play control again also stops it.
