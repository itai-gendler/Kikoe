---
kind: primary
routes:
  desktop: Desktop
steps:
- text: Start the microphone for the note.
  kind: actor
  entities:
  - entity: note
    effect: reads
    facts:
    - Title
  contexts:
    desktop:
      place: desktop::note
  actor: user
- text: Open the microphone and begin a microphone capture with the selected model and options.
  kind: product
  entities:
  - entity: microphone-capture
    effect: creates
    facts:
    - Destination
    - Started
    - Audio
    - Elapsed
    - Model and options
    - Confirmed text
    - Connection
    to: Recording
  - entity: preferences
    effect: reads
    facts:
    - Recent model
    - Requested features
    - Language
    - Custom vocabulary
    - Live transcription delay
    - Microphone
  - entity: model
    effect: reads
    facts: []
  contexts:
    desktop:
      place: desktop::note
  actor: user
- text: Retain accepted sound and confirmed text in the microphone capture while showing connection progress.
  kind: product
  entities:
  - entity: microphone-capture
    effect: changes
    facts:
    - Audio
    - Elapsed
    - Confirmed text
    - Connection
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

# Append microphone audio

## Trigger

The user starts capture in an open note.

## Outcome

Sound is retained while elapsed time and recognition progress are shown.

## Decision points

### Recognition mode

Which mode does the selected model provide?

- Realtime support → recognize accepted audio during capture and show provisional and confirmed text.
- File support only → keep capturing locally and explain that transcription follows Stop.
