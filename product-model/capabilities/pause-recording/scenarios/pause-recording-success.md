---
kind: primary
routes:
  desktop: Desktop
steps:
- text: Pause microphone capture.
  kind: actor
  entities:
  - entity: microphone-capture
    effect: reads
    facts: []
  contexts:
    desktop:
      place: desktop::note
  actor: user
- text: Pause microphone capture, freeze elapsed time and drain accepted live audio before closing its
    connection.
  kind: product
  entities:
  - entity: microphone-capture
    effect: changes
    facts:
    - Connection
    from: Recording
    to: Paused
  contexts:
    desktop:
      place: desktop::note
  actor: user
references:
- kind: code
  role: implementation
  target: src/kikoe/services/recording.py#RecordingSession.pause
- kind: code
  role: implementation
  target: src/kikoe/services/realtime.py
---

# Pause recording

## Trigger

The user pauses a running microphone recording.

## Outcome

The recording is Paused: the timer stops, no sound is kept, and a live connection finishes the audio it already has before closing.
