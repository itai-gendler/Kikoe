---
kind: primary
routes:
  desktop: Desktop
steps:
- text: Play the recording.
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
- text: Play original recording audio, ending any previous range.
  kind: product
  entities:
  - entity: recording
    effect: reads
    facts:
    - Original audio
  - entity: preferences
    effect: reads
    facts:
    - Audio output
  contexts:
    desktop:
      place: desktop::note
  actor: user
references:
- kind: code
  role: implementation
  target: src/kikoe/ui/speaker_controller.py
- kind: code
  role: implementation
  target: src/kikoe/services/playback.py
- kind: code
  role: implementation
  target: src/kikoe/core/speakers.py#sample_range
---

# Play original audio

## Trigger

The user starts playback of a saved audio section.

## Outcome

The retained recording plays on the selected output device.

## Edge cases

- Missing original audio or an output error is explained.
- Switching notes or beginning conflicting work ends playback.
