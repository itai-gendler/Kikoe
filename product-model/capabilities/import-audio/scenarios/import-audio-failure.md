---
kind: edge
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
- text: Conversion or transcription fails.
  kind: condition
  entities: []
  contexts:
    desktop:
      place: desktop::note
- text: Remove provisional output and explain the failure.
  kind: product
  entities: []
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

# Leave the library unchanged on import failure

## Trigger

Conversion or any transcription request fails.

## Outcome

No new note or recording is saved. Temporary preview and the copied original are removed; an existing note is unchanged.

## Edge cases

- Missing audio, unreadable responses, request rejection and network failures are reported.
- A truncated or filtered Audio LLM or MiMo reply is not accepted as completed text.
- Output-length rejection suggests reducing chunk length or size.
