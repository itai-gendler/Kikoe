---
kind: alternate
routes:
  desktop: Desktop
steps:
- text: Close Kikoe during microphone capture.
  kind: actor
  entities:
  - entity: microphone-capture
    effect: reads
    facts: []
  contexts:
    desktop:
      place: desktop::note
  actor: user
- text: Stop microphone capture and finish accepted audio.
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
- text: Retain the recording and release microphone capture after saving.
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
  - entity: note
    effect: changes
    facts:
    - Recordings
    - Duration
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
  target: src/kikoe/ui/window.py#Window._save_and_close
- kind: code
  role: implementation
  target: src/kikoe/services/activity.py#ActivityTracker.wind_down
- kind: code
  role: implementation
  target: src/kikoe/services/recording_workflow.py
---

# Keep microphone audio while closing

## Trigger

The user quits during microphone capture.

## Outcome

Local audio and confirmed text are retained; closing does not start a new file upload.

## Edge cases

- An incomplete live session is saved as incomplete.
- Interrupted finalization leaves material for startup recovery.
