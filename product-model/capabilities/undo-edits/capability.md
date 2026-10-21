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

# Undo edits

Step back through the open note’s saved text and timing edits, one step at a time, saving each restored value.
