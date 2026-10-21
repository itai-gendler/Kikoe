---
kind: edge
routes:
  desktop: Desktop
steps:
- text: Start the microphone.
  kind: actor
  entities: []
  contexts:
    desktop:
      place: desktop::note
  actor: user
- text: The microphone or required media tool cannot start.
  kind: condition
  entities: []
  contexts:
    desktop:
      place: desktop::note
- text: Explain the startup failure.
  kind: product
  entities: []
  contexts:
    desktop:
      place: desktop::note
  actor: user
references:
- kind: code
  role: implementation
  target: src/kikoe/services/recording_workflow.py
- kind: code
  role: implementation
  target: src/kikoe/services/recording.py
- kind: code
  role: implementation
  target: src/kikoe/services/realtime.py
---

# Explain a capture startup failure

## Trigger

The user starts recording, but the microphone or ffmpeg cannot start.

## Outcome

An error is shown; failed microphone startup does not leave a new empty note.
