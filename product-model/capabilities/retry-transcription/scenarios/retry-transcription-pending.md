---
kind: alternate
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
- text: Complete the pending recording using the selected file model.
  kind: product
  entities:
  - entity: recording
    effect: changes
    facts:
    - Transcript
    - Timestamps
    - Speaker assignments
    - Provider and model
    from: Pending
    to: Ready
  - entity: model
    effect: reads
    facts: []
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

# Transcribe recovered pending audio

## Trigger

Recovered audio is pending and the user chooses Retry Transcription.

## Outcome

The original recording is completed in place.
