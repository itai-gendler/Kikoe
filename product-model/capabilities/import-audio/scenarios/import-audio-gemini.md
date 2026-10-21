---
kind: alternate
routes:
  desktop: Desktop
steps:
- text: Choose audio for transcription.
  kind: actor
  entities: []
  contexts:
    desktop:
      place: desktop::note
  actor: user
- text: Read the selected model options and provider configuration.
  kind: condition
  entities:
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
  - entity: preferences
    effect: reads
    facts:
    - Language
    - Custom vocabulary
    - Requested features
  contexts:
    desktop:
      place: desktop::note
- text: Split requests to at most thirty minutes when annotated, or sixty minutes otherwise, subject to
    stricter user limits.
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
  target: src/kikoe/providers/gemini.py#GeminiClient.upload_limits
- kind: code
  role: implementation
  target: src/kikoe/services/importer.py
---

# Respect Gemini annotated duration

## Trigger

Gemini is selected for a file with timestamps or speakers.

## Outcome

Each request carries at most thirty minutes of audio when timestamps or speakers are requested, or sixty otherwise, and less when the provider’s Chunk Length is shorter.
