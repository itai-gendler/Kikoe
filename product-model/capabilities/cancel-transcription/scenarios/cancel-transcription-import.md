---
kind: primary
routes:
  desktop: Desktop
steps:
- text: Cancel conversion or transcription.
  kind: actor
  entities: []
  contexts:
    desktop:
      place: desktop::note
  actor: user
- text: Show cancellation in progress until workers and temporary resources are released.
  kind: product
  entities: []
  contexts:
    desktop:
      place: desktop::note
  actor: user
references:
- kind: code
  role: implementation
  target: src/kikoe/ui/transcription_controller.py#TranscriptionController.on_cancel_import
- kind: code
  role: implementation
  target: src/kikoe/services/importer.py
- kind: code
  role: implementation
  target: src/kikoe/services/file_transcription.py
- kind: code
  role: implementation
  target: src/kikoe/services/commits.py
---

# Cancel an import

## Trigger

The user cancels while a file is converting or transcribing.

## Outcome

The preview and copied original are removed and no imported item is saved.
