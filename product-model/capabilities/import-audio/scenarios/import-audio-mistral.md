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
- text: Omit the language hint, request automatic detection, send custom vocabulary, and keep only requested
    transcript annotations.
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
  target: src/kikoe/providers/mistral.py
- kind: code
  role: implementation
  target: src/kikoe/core/choice.py#language_dropped
---

# Use Mistral transcription options

## Trigger

Mistral is selected with a language hint and timestamps or speakers.

## Outcome

The request leaves the language out so Mistral detects it and sends the custom vocabulary; the saved recording keeps only the requested timestamps or speakers.
