---
kind: primary
routes:
  desktop: Desktop
steps:
- text: Retry transcription of the recording.
  kind: actor
  entities:
  - entity: recording
    effect: reads
    facts:
    - Original audio
  contexts:
    desktop:
      place: desktop::note
  actor: user
- text: Mark the recording pending while transcription runs.
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
- text: Replace the recording result.
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

# Replace incomplete text after retry

## Trigger

The user retries an incomplete recording with a file model.

## Outcome

The same recording is ready; its transcript and model attribution are replaced on complete success.
