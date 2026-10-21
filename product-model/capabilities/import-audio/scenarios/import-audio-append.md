---
kind: primary
routes:
  desktop: Desktop
steps:
- text: Choose audio for the note.
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
- text: Prepare audio for the selected model and show transcription progress.
  kind: product
  entities:
  - entity: preferences
    effect: reads
    facts:
    - Recent model
    - Requested features
    - Language
  - entity: model
    effect: reads
    facts:
    - Model ID
    - Display name
    - File support
    - Realtime support
  - entity: provider
    effect: reads
    facts:
    - Name
    - API type
    - Base URL
    - API key
    - Upload settings
    - Audio LLM settings
  contexts:
    desktop:
      place: desktop::note
  actor: user
- text: Save the recording and extend the note.
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
  target: src/kikoe/ui/transcription_controller.py
- kind: code
  role: implementation
  target: src/kikoe/services/importer.py
- kind: code
  role: implementation
  target: src/kikoe/core/upload.py
---

# Append a transcribed file

## Trigger

The user chooses an audio file with an open note.

## Outcome

One ready recording is appended, with original audio and all completed transcript chunks in source order.

## Edge cases

- Large inputs are split using the stricter size and duration budget, with timestamps shifted into source time.
- Streaming preview shows only the contiguous completed prefix and current unfinished text.
- Text, playback and matching are unavailable on provisional preview rows.
