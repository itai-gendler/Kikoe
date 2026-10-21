---
appliesTo:
- type: capability
  id: edit-transcript
- type: capability
  id: undo-edits
- type: capability
  id: redo-edits
- type: capability
  id: export-note
- type: capability
  id: copy-all-text
- type: capability
  id: close-kikoe
references:
- kind: code
  role: implementation
  target: src/kikoe/core/edit_history.py
- kind: code
  role: implementation
  target: src/kikoe/services/editing.py
---

# Undo history belongs to the open note

History covers passage text and timing. It groups consecutive text-only changes to one passage less than two seconds apart until the group is sealed. New edits discard redo; changing notes or incompatible transcript replacement clears history. Exports and close wait for submitted edits.
