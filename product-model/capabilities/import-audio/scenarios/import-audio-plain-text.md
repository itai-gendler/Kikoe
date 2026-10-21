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
- text: Produce plain text without timing or attribution, using the configured prompt and request format
    for Audio LLM.
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
  target: src/kikoe/providers/mimo.py
- kind: code
  role: implementation
  target: src/kikoe/providers/audio_llm.py
- kind: code
  role: implementation
  target: src/kikoe/providers/audio_llm_gemini.py
---

# Use prompted or plain-text recognition

## Trigger

MiMo or an Audio LLM model is selected.

## Outcome

The recording is plain text without timestamps or speakers; Audio LLM requests use the provider’s prompt and request format.
