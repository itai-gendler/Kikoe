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
- text: End microphone capture and finish accepted audio.
  kind: product
  entities:
  - entity: microphone-capture
    effect: changes
    facts:
    - Audio
    - Elapsed
    from: Recording
    to: Stopped
  contexts:
    desktop:
      place: desktop::note
  actor: user
- text: Save a recording with retained audio and confirmed text, and release the microphone capture.
  kind: product
  entities:
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
  - entity: microphone-capture
    effect: removes
    from: Stopped
  - entity: note
    effect: changes
    facts:
    - Recordings
    - Duration
  contexts:
    desktop:
      place: desktop::note
  actor: user
- text: Mark the recording incomplete while retaining its original audio and confirmed transcript.
  kind: product
  entities:
  - entity: recording
    effect: changes
    facts:
    - Transcript
    - Timestamps
    - Speaker assignments
    from: Pending
    to: Incomplete
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

# Keep incomplete live audio

## Trigger

The user stops a live recording whose recognition did not finish.

## Outcome

Kikoe waits at most ten seconds for final text, keeps the audio and confirmed text, and marks the recording Incomplete with Retry Transcription offered; no second upload starts.
