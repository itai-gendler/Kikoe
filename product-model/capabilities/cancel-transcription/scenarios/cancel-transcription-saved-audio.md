---
kind: alternate
routes:
  desktop: Desktop
steps:
- text: Cancel work on a recording.
  kind: actor
  entities:
  - entity: recording
    effect: reads
    facts:
    - Original audio
    - Transcript
  contexts:
    desktop:
      place: desktop::note
  actor: user
- text: Finish cleanup and keep the recording content.
  kind: product
  entities:
  - entity: recording
    effect: reads
    facts:
    - Created
    - Source
    - Duration
    - Original audio
    - Provider and model
    - Transcript
    - Timestamps
    - Speaker assignments
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

# Cancel work on retained audio

## Trigger

The user cancels a retry or re-transcription.

## Outcome

Existing audio and text survive. Retry ends incomplete; re-transcription preserves its original status.

## Edge cases

- Once final saving begins, cancellation is unavailable and close waits for the save result.
