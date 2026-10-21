---
kind: primary
result: achieved
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
  capability: import-audio
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
  capability: import-audio
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
  capability: import-audio
- text: Edit recording transcript text.
  kind: actor
  entities:
  - entity: recording
    effect: reads
    facts:
    - Transcript
  contexts:
    desktop:
      place: desktop::note
  actor: user
  capability: edit-transcript
- text: Save the edited recording passage and remember the edit for Undo.
  kind: product
  entities:
  - entity: recording
    effect: changes
    facts:
    - Transcript
  contexts:
    desktop:
      place: desktop::note
  actor: user
  capability: edit-transcript
references:
- kind: code
  role: implementation
  target: src/kikoe/ui/transcription_controller.py#TranscriptionController._import
- kind: code
  role: implementation
  target: src/kikoe/ui/segment_editor.py
---

# Review an imported note

## Trigger

The user imports audio without an open note.

## Outcome

The completed note opens and the user saves a refinement to its transcript.
