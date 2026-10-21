---
kind: edge
routes:
  desktop: Desktop
steps:
- text: Choose audio for transcription.
  kind: actor
  actor: user
  entities: []
  contexts:
    desktop:
      place: desktop::note
- text: The external service rejects the request or is unavailable.
  kind: condition
  entities: []
  contexts:
    desktop:
      place: desktop::note
- text: Explain the service failure and remove provisional output without adding library content.
  kind: product
  actor: user
  entities: []
  contexts:
    desktop:
      place: desktop::note
references:
- kind: code
  role: implementation
  target: src/kikoe/providers/errors.py#status_error
- kind: code
  role: implementation
  target: src/kikoe/services/importer.py#import_audio
---

# Explain external service rejection

## Trigger

A cloud request is refused or cannot finish.

## Outcome

Kikoe reports the external cause without saving a partial import.

## Edge cases

- A rejected credential directs the user to connection settings.
- Model or regional access refusal belongs to the external service account.
- Exhausted credits, throttling or quota exhaustion are explained separately.
- Missing models, oversized audio, timeout and server failures receive their own explanations.
