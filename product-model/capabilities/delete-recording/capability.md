---
availability:
- place: desktop
references:
- kind: code
  role: implementation
  target: src/kikoe/ui/note_actions.py#NoteActions.on_delete_recording
- kind: code
  role: implementation
  target: src/kikoe/storage/library.py#Library.delete_recording
domain: notes
---

# Delete recording

Permanently remove one audio section, its transcript and original audio, keeping the surrounding note.
