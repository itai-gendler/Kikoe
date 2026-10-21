---
kind: alternate
routes:
  desktop: Desktop
steps:
- text: Play a recording sample for a speaker.
  kind: actor
  entities:
  - entity: recording
    effect: reads
    facts:
    - Original audio
    - Transcript
    - Timestamps
    - Speaker assignments
  - entity: speaker
    effect: reads
    facts:
    - Name
    - Number
  contexts:
    desktop:
      place: desktop::note
  actor: user
- text: Play the recording range on the selected output.
  kind: product
  entities:
  - entity: recording
    effect: reads
    facts:
    - Original audio
    - Timestamps
    - Duration
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

# Hear a speaker sample

## Trigger

The user listens to a quoted turn while matching speakers.

## Outcome

A reliably timed sample plays for at most ten seconds, bounded by the turn and recording end.

## Edge cases

- Without a reliable start and end range, the quotation remains useful but sample playback is unavailable.
