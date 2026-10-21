---
kind: alternate
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
- text: Finish the recording with complete transcription.
  kind: product
  entities:
  - entity: recording
    effect: changes
    facts:
    - Transcript
    - Timestamps
    - Speaker assignments
    from: Pending
    to: Ready
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

# Transcribe after Stop

## Trigger

The user stops a recording whose model transcribes files only.

## Outcome

The saved audio is transcribed with the model and options chosen when recording started, and the recording is Ready.
