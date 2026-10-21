---
kind: alternate
routes:
  desktop: Desktop
steps:
- text: Choose an audio file.
  kind: actor
  entities: []
  contexts:
    desktop:
      place: desktop::note
  actor: user
- text: Transcribe every audio part, then create the note and its recording together.
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
    to: Ready
    with: note
  contexts:
    desktop:
      place: desktop::note
  actor: user
- text: Open the saved note and its recording.
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
  target: src/kikoe/ui/transcription_controller.py
- kind: code
  role: implementation
  target: src/kikoe/services/importer.py
- kind: code
  role: implementation
  target: src/kikoe/core/upload.py
---

# Create a note from an audio file

## Trigger

No note is open when the user imports audio.

## Outcome

After complete success a note named after the file is created and opened.
