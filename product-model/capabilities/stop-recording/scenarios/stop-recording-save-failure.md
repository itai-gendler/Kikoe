---
kind: edge
routes:
  desktop: Desktop
steps:
- text: Stop the microphone capture.
  kind: actor
  actor: user
  entities:
  - entity: microphone-capture
    effect: reads
    facts: []
  contexts:
    desktop:
      place: desktop::note
- text: Finish accepted microphone capture audio.
  kind: product
  actor: user
  entities:
  - entity: microphone-capture
    effect: changes
    from: Recording
    to: Stopped
    facts:
    - Audio
    - Elapsed
  contexts:
    desktop:
      place: desktop::note
- text: Local conversion or saving cannot complete.
  kind: condition
  entities: []
  contexts:
    desktop:
      place: desktop::note
- text: Report the error and retain the unfinished microphone capture for recovery.
  kind: product
  actor: user
  entities:
  - entity: microphone-capture
    effect: changes
    from: Stopped
    to: Interrupted
    facts:
    - Audio
    - Confirmed text
  contexts:
    desktop:
      place: desktop::note
references:
- kind: code
  role: implementation
  target: src/kikoe/services/recovery.py#recover_recording
- kind: code
  role: implementation
  target: src/kikoe/services/recording_workflow.py#RecordingWorkflow._save
---

# Retain audio when finalization fails

## Trigger

The user stops recording, but converting or saving the audio fails.

## Outcome

The error is shown and the unfinished recording stays Interrupted, to be offered for recovery at the next startup; no recording is added to the note yet.
