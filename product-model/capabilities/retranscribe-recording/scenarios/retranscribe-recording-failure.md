---
kind: edge
routes:
  desktop: Desktop
steps:
- text: Start replacement transcription.
  kind: actor
  entities: []
  contexts:
    desktop:
      place: desktop::note
  actor: user
- text: The replacement fails or is cancelled.
  kind: condition
  entities: []
  contexts:
    desktop:
      place: desktop::note
- text: Restore the original recording presentation and report the outcome.
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
  target: src/kikoe/ui/retranscribe_dialog.py
- kind: code
  role: implementation
  target: src/kikoe/services/file_transcription.py#FileTranscriptionWorkflow.retranscribe
- kind: code
  role: implementation
  target: src/kikoe/storage/library.py#Library.update_transcription
---

# Keep the previous transcript

## Trigger

The replacement transcription fails or is cancelled.

## Outcome

Old text, identities, status, audio and model attribution are retained; the preview disappears.
