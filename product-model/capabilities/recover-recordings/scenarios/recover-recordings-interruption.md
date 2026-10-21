---
kind: edge
routes:
  desktop: Desktop
steps:
- text: Microphone capture is interrupted before finalization.
  kind: condition
  entities:
  - entity: microphone-capture
    effect: reads
    facts:
    - Destination
    - Started
    - Audio
    - Elapsed
    - Model and options
    - Confirmed text
    - Connection
  contexts:
    desktop:
      place: desktop::note
  unattended: true
- text: Keep accepted audio and confirmed microphone capture text for recovery.
  kind: product
  entities:
  - entity: microphone-capture
    effect: changes
    facts:
    - Audio
    - Elapsed
    - Confirmed text
    from: Recording
    to: Interrupted
  contexts:
    desktop:
      place: desktop::note
references:
- kind: code
  role: implementation
  target: src/kikoe/storage/captures.py
- kind: code
  role: implementation
  target: src/kikoe/services/recording.py
---

# Retain recovery material after interruption

## Trigger

The application stops before microphone finalization completes.

## Outcome

The unfinished session remains recoverable on startup.
