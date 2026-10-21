---
kind: edge
routes:
  desktop: Desktop
steps:
- text: Retry transcription.
  kind: actor
  entities: []
  contexts:
    desktop:
      place: desktop::note
  actor: user
- text: Begin work on the recording.
  kind: product
  entities:
  - entity: recording
    effect: changes
    facts: []
    from: Incomplete
    to: Pending
  contexts:
    desktop:
      place: desktop::note
  actor: user
- text: Report failure and retain the recording content.
  kind: product
  entities:
  - entity: recording
    effect: changes
    facts: []
    from: Pending
    to: Incomplete
  contexts:
    desktop:
      place: desktop::note
  actor: user
references:
- kind: code
  role: implementation
  target: src/kikoe/ui/transcription_controller.py#TranscriptionController._retry
- kind: code
  role: implementation
  target: src/kikoe/services/file_transcription.py#FileTranscriptionWorkflow.transcribe_pending
---

# Retain an unsuccessful retry

## Trigger

A retry fails or the user cancels it.

## Outcome

The recording is incomplete and keeps previous text and retained audio.
