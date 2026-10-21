---
availability:
- place: desktop
references:
- kind: code
  role: implementation
  target: src/kikoe/core/edit_history.py#EditHistory
- kind: code
  role: implementation
  target: src/kikoe/services/editing.py#EditingSession
domain: notes
---

# Redo edits

Reapply edits that Undo stepped back through in the open note, saving each reapplied value.
