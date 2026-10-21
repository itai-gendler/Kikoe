---
kind: alternate
routes:
  desktop: Desktop
steps:
- text: Export the note as subtitles.
  kind: actor
  entities:
  - entity: note
    effect: reads
    facts:
    - Title
    - Display options
  contexts:
    desktop:
      place: desktop::note
  actor: user
- text: Render recording text, timestamps and selected speaker labels into subtitles.
  kind: product
  entities:
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
  - entity: speaker
    effect: reads
    facts:
    - Name
    - Number
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
- text: Choose a destination.
  kind: actor
  entities: []
  contexts:
    desktop:
      place: desktop::note
  actor: user
- text: Write the subtitle file.
  kind: product
  entities: []
  contexts:
    desktop:
      place: desktop::note
  actor: user
references:
- kind: code
  role: implementation
  target: src/kikoe/ui/export_controller.py
- kind: code
  role: implementation
  target: src/kikoe/ui/export_dialog.py
- kind: code
  role: implementation
  target: src/kikoe/core/export.py
---

# Export one continuous subtitle track

## Trigger

The note contains timestamp information and the user chooses SRT or WebVTT.

## Outcome

Timestamps are always exported; recording durations offset later sections into one continuous subtitle track.

## Edge cases

- The timestamp switch cannot leave times out of subtitles.
- A partially timed note can be exported: an untimed passage starts where the previous cue ended, and a missing end uses the next later start or lasts two seconds.
- A cue that would end at or before its start is given a positive length.
- Blank passages are skipped.
