---
kind: alternate
routes:
  desktop: Desktop
steps:
- text: Choose another note from the existing list.
  kind: actor
  entities:
  - entity: note
    effect: reads
    facts:
    - Title
  contexts:
    desktop:
      place: desktop::notes
  actor: user
- text: Show that note and its recording text while work continues on the original target.
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
  target: src/kikoe/core/activity.py#Activity.switch_locked
- kind: code
  role: implementation
  target: src/kikoe/ui/transcription_controller.py#TranscriptionController._import
- kind: code
  role: implementation
  target: src/kikoe/ui/window.py#Window._open_note
---

# Open another note during file transcription

## Trigger

A file transcription is running and the user selects another saved item.

## Outcome

The selected note is usable while the other task continues. Completion does not pull the user back to the transcription target.
