---
kind: edge
routes:
  desktop: Desktop
steps:
- text: Stop microphone capture.
  kind: actor
  entities:
  - entity: microphone-capture
    effect: reads
    facts: []
  contexts:
    desktop:
      place: desktop::note
  actor: user
- text: Finish microphone capture and retain its recording before transcription.
  kind: product
  entities:
  - entity: microphone-capture
    effect: changes
    facts:
    - Audio
    - Elapsed
    from: Recording
    to: Stopped
  - entity: recording
    effect: creates
    facts:
    - Created
    - Source
    - Duration
    - Original audio
    - Provider and model
    - Transcript
    - Timestamps
    - Speaker assignments
    to: Pending
  - entity: note
    effect: changes
    facts:
    - Recordings
    - Duration
  contexts:
    desktop:
      place: desktop::note
  actor: user
- text: Report the transcription failure and retain the recording.
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
- text: Release the finalized microphone capture.
  kind: product
  entities:
  - entity: microphone-capture
    effect: removes
    from: Stopped
  contexts:
    desktop:
      place: desktop::note
  actor: user
references:
- kind: code
  role: implementation
  target: src/kikoe/services/recording_workflow.py
- kind: code
  role: implementation
  target: src/kikoe/services/recovery.py
- kind: code
  role: implementation
  target: src/kikoe/services/file_transcription.py
---

# Keep audio when transcription after Stop fails

## Trigger

The recording is saved after Stop, but its transcription fails.

## Outcome

The original audio stays in the note and the recording is Incomplete, ready for Retry Transcription with a file model.
