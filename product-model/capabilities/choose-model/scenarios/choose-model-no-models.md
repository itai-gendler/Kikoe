---
kind: validation
routes:
  desktop: Desktop
steps:
- text: Open the transcription picker.
  kind: actor
  entities: []
  contexts:
    desktop:
      place: desktop::transcription-model
  actor: user
- text: No transcription choice is available.
  kind: condition
  entities: []
  contexts:
    desktop:
      place: desktop::transcription-model
- text: Offer configuration.
  kind: product
  entities: []
  contexts:
    desktop:
      place: desktop::transcription-model
  actor: user
references:
- kind: code
  role: implementation
  target: src/kikoe/ui/bottom_bar.py
- kind: code
  role: implementation
  target: src/kikoe/ui/transcription_dialog.py
- kind: code
  role: implementation
  target: src/kikoe/core/choice.py
---

# Show that no models are available

## Trigger

No configured or installed local speech model is available.

## Outcome

The picker explains the missing setup and offers provider and model management.
