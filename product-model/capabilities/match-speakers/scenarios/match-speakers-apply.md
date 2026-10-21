---
kind: primary
routes:
  desktop: Desktop
steps:
- text: Review recording quotations and speaker candidates.
  kind: actor
  entities:
  - entity: recording
    effect: reads
    facts:
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
- text: Choose existing identities or Keep as New Speaker.
  kind: actor
  entities:
  - entity: speaker
    effect: reads
    facts: []
  contexts:
    desktop:
      place: desktop::note
  actor: user
- text: Save the recording speaker assignments together.
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

# Confirm speaker identities

## Trigger

An appended or replaced recording has unconfirmed identities.

## Outcome

All applied choices are confirmed, including keeping new identities separate; the next unresolved recording can be offered.

## Edge cases

- Multiple source labels may map to the same person.
- Named identities retained after re-transcription remain candidates.
- Cancel writes nothing; stale candidates produce an explanatory error.
