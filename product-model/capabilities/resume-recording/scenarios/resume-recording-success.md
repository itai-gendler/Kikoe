---
kind: primary
routes:
  desktop: Desktop
steps:
- text: Resume microphone capture.
  kind: actor
  entities:
  - entity: microphone-capture
    effect: reads
    facts: []
  contexts:
    desktop:
      place: desktop::note
  actor: user
- text: Continue microphone capture audio and elapsed time; live recognition starts a new connection from
    confirmed audio.
  kind: product
  entities:
  - entity: microphone-capture
    effect: changes
    facts:
    - Audio
    - Elapsed
    - Connection
    from: Paused
    to: Recording
  contexts:
    desktop:
      place: desktop::note
  actor: user
references:
- kind: code
  role: implementation
  target: src/kikoe/services/recording.py#RecordingSession.resume
- kind: code
  role: implementation
  target: src/kikoe/services/realtime.py
---

# Resume recording

## Trigger

The user resumes a paused recording.

## Outcome

The same recording continues without the pause in its audio or duration; live recognition reconnects from the confirmed audio with a new speaker-label scope.
