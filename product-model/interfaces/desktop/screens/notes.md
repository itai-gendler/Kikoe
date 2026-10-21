---
entities:
- entity: note
  shows:
  - Title
  - Created
  - Recordings
  - Duration
  collects:
  - Title
references:
- kind: code
  role: implementation
  target: src/kikoe/ui/note_sidebar.py
- kind: code
  role: implementation
  target: src/kikoe/ui/new_note_dialog.py
---

# Notes

Browse the saved library, search titles and transcript text, and create a named note.
