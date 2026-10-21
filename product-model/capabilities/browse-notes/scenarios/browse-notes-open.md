---
kind: primary
routes:
  desktop: Desktop
steps:
- text: Read note titles and durations.
  kind: actor
  entities:
  - entity: note
    effect: reads
    facts:
    - Title
    - Created
    - Duration
    - Recordings
  contexts:
    desktop:
      place: desktop::notes
  actor: user
- text: Select the note.
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
- text: Show the note, each recording and its speaker names.
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
  - entity: speaker
    effect: reads
    facts:
    - Name
    - Number
  contexts:
    desktop:
      place: desktop::note
  actor: user
references:
- kind: code
  role: implementation
  target: src/kikoe/ui/note_sidebar.py
- kind: code
  role: implementation
  target: src/kikoe/storage/library.py#Library.search_notes
- kind: code
  role: implementation
  target: src/kikoe/ui/window.py
---

# Open a saved note

## Trigger

The user chooses a saved item.

## Outcome

The selected note shows its recordings, text and speakers.
