---
kind: primary
routes:
  desktop: Desktop
steps:
- text: Confirm replacement of recording text, including manual edits.
  kind: actor
  entities:
  - entity: recording
    effect: reads
    facts:
    - Transcript
    - Original audio
  contexts:
    desktop:
      place: desktop::note
  actor: user
- text: Transcribe retained audio and replace the recording result atomically.
  kind: product
  entities:
  - entity: recording
    effect: changes
    facts:
    - Transcript
    - Timestamps
    - Speaker assignments
    - Provider and model
    from: Ready
    to: Ready
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

# Replace a recording transcript

## Trigger

The user confirms a file model and options for an existing recording.

## Outcome

The new result replaces text, times, speaker assignments and model attribution only after complete success.

## Edge cases

- A successful empty transcript replaces the old text with an empty ready result.
- Strong, unambiguous timing overlap preserves speaker names; uncertain assignments need matching.
- No retained audio means replacement cannot begin.
- A live-only current choice requires explicitly choosing a file model.
