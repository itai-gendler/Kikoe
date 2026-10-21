---
kind: alternate
routes:
  desktop: Desktop
steps:
- text: Close Kikoe.
  kind: actor
  entities: []
  contexts:
    desktop:
      place: desktop::note
  actor: user
- text: End cancellable file work, await final saving or active recovery, and retain previously saved
    note and recording content.
  kind: product
  entities:
  - entity: note
    effect: reads
    facts:
    - Title
    - Created
    - Recordings
    - Duration
    - Display options
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
  target: src/kikoe/ui/window.py#Window._save_and_close
- kind: code
  role: implementation
  target: src/kikoe/services/activity.py#ActivityTracker.wind_down
- kind: code
  role: implementation
  target: src/kikoe/services/recording_workflow.py
---

# Close during transcription or recovery

## Trigger

The user closes Kikoe while file work or recovery is active.

## Outcome

Cancellable file work ends with its preservation policy; a final save or active recovery completes before close.

## Edge cases

- A close-time saving error is reported and the window remains open.
