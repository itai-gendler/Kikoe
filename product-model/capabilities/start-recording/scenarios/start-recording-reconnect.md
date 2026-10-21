---
kind: edge
routes:
  desktop: Desktop
steps:
- text: A live connection fails during microphone capture.
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
- text: Retain microphone capture audio and show reconnecting or incomplete recognition.
  kind: product
  entities:
  - entity: microphone-capture
    effect: changes
    facts:
    - Audio
    - Elapsed
    - Connection
  contexts:
    desktop:
      place: desktop::note
- text: On reconnection, replay the unconfirmed audio and replace provisional text with confirmed microphone
    capture text.
  kind: product
  entities:
  - entity: microphone-capture
    effect: changes
    facts:
    - Confirmed text
    - Connection
  contexts:
    desktop:
      place: desktop::note
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

# Continue capture through a live connection failure

## Trigger

A live recognition connection fails during capture.

## Outcome

Audio continues to be retained; retryable failures reconnect and catch up from the confirmed position. Unrecoverable recognition failure is shown while local capture remains available.

## Edge cases

- Stop ends reconnection waiting so that local audio can be saved.
- A new recognition connection receives a separate speaker-label scope.
