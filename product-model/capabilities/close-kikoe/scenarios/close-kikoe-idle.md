---
kind: primary
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
- text: Wait for recording text and timing edits and stop audio playback.
  kind: product
  entities:
  - entity: recording
    effect: reads
    facts:
    - Transcript
    - Timestamps
    - Original audio
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

# Close after saving edits

## Trigger

The user closes Kikoe while no capture or transcription is running.

## Outcome

Pending edits finish and playback ends before the window closes.
