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
- text: Save the recording annotations with independent speaker identities and append it to the note.
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
  - entity: speaker
    effect: creates
    facts:
    - Name
    - Number
  contexts:
    desktop:
      place: desktop::note
  actor: user
references:
- kind: code
  role: implementation
  target: src/kikoe/providers/deepgram.py
- kind: code
  role: implementation
  target: src/kikoe/providers/openai.py
- kind: code
  role: implementation
  target: src/kikoe/providers/openrouter.py
- kind: code
  role: implementation
  target: src/kikoe/providers/groq.py
---

# Use a model with timestamps and speakers

## Trigger

The chosen Deepgram, OpenAI, OpenRouter or other file model supports the requested annotations.

## Outcome

The recording keeps the requested timestamps in source time, and its speaker labels become speakers of the note, kept apart from other recordings’ speakers until matched.
