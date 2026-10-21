---
kind: alternate
routes:
  desktop: Desktop
steps:
- text: Choose an audio file.
  kind: actor
  entities: []
  contexts:
    desktop:
      place: desktop::note
  actor: user
- text: Read the local model language requirement and the local engine device selection.
  kind: product
  entities:
  - entity: local-model
    effect: reads
    facts:
    - Name
    - Size
    - Languages
    - Features
    - Purpose
    - Download progress
    - Engine availability
  - entity: local-engine
    effect: reads
    facts:
    - Name
    - Version
    - Acceleration
    - Device
    - Download progress
    - Readiness
    - Included with Kikoe
  - entity: preferences
    effect: reads
    facts:
    - Language
  contexts:
    desktop:
      place: desktop::note
  actor: user
- text: Recognize the audio locally and append the recording to the note.
  kind: product
  entities:
  - entity: recording
    effect: creates
    facts:
    - Created
    - Source
    - Duration
    - Original audio
    - Provider and model
    - Transcript
    - Timestamps
    - Speaker assignments
    to: Ready
  - entity: note
    effect: changes
    facts:
    - Recordings
    - Duration
  contexts:
    desktop:
      place: desktop::note
  actor: user
references:
- kind: code
  role: implementation
  target: src/kikoe/providers/local/client.py
- kind: code
  role: implementation
  target: src/kikoe/services/importer.py
---

# Transcribe audio on this device

## Trigger

The selected local speech model and engine are installed.

## Outcome

The retained audio is transcribed locally with no cloud upload.

## Edge cases

- A missing engine or model is explained and the import does not commit.
- A model requiring an explicit language rejects missing or unsupported language choices.
- An installed speaker-detection model can add speakers to a timestamp-capable local model.
