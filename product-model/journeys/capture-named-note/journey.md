---
actors:
- user
references:
- kind: code
  role: implementation
  target: src/kikoe/ui/note_actions.py#NoteActions._create_note
- kind: code
  role: implementation
  target: src/kikoe/ui/recording_controller.py
---

# Capture in a named note

## Goal

The user names a new note and records into it.

## Success criterion

The named note contains retained audio and the complete live transcript after capture is stopped.
