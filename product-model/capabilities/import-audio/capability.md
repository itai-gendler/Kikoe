---
availability:
- place: desktop
references:
- kind: code
  role: implementation
  target: src/kikoe/ui/transcription_controller.py
- kind: code
  role: implementation
  target: src/kikoe/services/importer.py
- kind: code
  role: implementation
  target: src/kikoe/core/upload.py
domain: notes
---

# Import audio

Transcribe an existing audio file and append it to the open note, or create a note named after the file. Retain a copy of the original only when the import succeeds.
