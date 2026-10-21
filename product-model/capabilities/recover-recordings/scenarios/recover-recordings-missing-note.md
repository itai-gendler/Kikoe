---
kind: alternate
routes:
  desktop: Desktop
steps:
- text: Choose Recover for the unfinished sessions.
  kind: actor
  entities: []
  contexts:
    desktop:
      place: desktop
  actor: user
- text: Create a note with the saved title and its recovered recording, then release the microphone capture.
  kind: product
  entities:
  - entity: note
    effect: creates
    facts:
    - Title
    - Created
    - Recordings
    - Duration
    - Display options
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
    with: note
  - entity: microphone-capture
    effect: removes
    from: Interrupted
  contexts:
    desktop:
      place: desktop
  actor: user
- text: Open the recovered note.
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
  contexts:
    desktop:
      place: desktop::note
  actor: user
references:
- kind: code
  role: implementation
  target: src/kikoe/ui/recording_controller.py#RecordingController.offer_recovery
- kind: code
  role: implementation
  target: src/kikoe/services/recovery.py
---

# Recover after the original note was removed

## Trigger

The interrupted capture points to a note that no longer exists.

## Outcome

A new note with the captured title receives the recording; recovery still performs no upload.
