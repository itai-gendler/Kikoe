---
actors:
- user
references:
- kind: code
  role: implementation
  target: src/kikoe/ui/transcription_controller.py#TranscriptionController._import
- kind: code
  role: implementation
  target: src/kikoe/ui/segment_editor.py
---

# Review an imported note

## Goal

The user imports audio without an open note.

## Success criterion

The completed note opens and the user saves a refinement to its transcript.
