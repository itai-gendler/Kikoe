---
kind: alternate
routes:
  desktop: Desktop
steps:
- text: Enter a search query.
  kind: actor
  entities: []
  contexts:
    desktop:
      place: desktop::notes
  actor: user
- text: Match note titles and recording transcript text without regard to case.
  kind: product
  entities:
  - entity: note
    effect: reads
    facts:
    - Title
  - entity: recording
    effect: reads
    facts:
    - Transcript
  contexts:
    desktop:
      place: desktop::notes
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

# Find words in a title or transcript

## Trigger

The user enters a search query.

## Outcome

Matching notes are shown without changing the open note; a blank query restores all notes.

## Edge cases

- No matches show No Matching Notes.
- Search is unavailable while a recording or transcription runs.
