---
appliesTo:
- type: entity
  id: note
- type: entity
  id: recording
references:
- kind: code
  role: implementation
  target: src/kikoe/ui/display_actions.py
- kind: code
  role: implementation
  target: src/kikoe/ui/export_dialog.py
- kind: code
  role: implementation
  target: src/kikoe/core/export.py
---

# Display options do not alter transcript facts

Timestamp and speaker display options are kept per note and initialize clipboard and export formatting. They never remove stored timing or identities. Subtitle output always includes times, and the desktop offers it only when the note contains timestamp information.
