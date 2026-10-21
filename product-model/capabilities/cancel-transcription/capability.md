---
availability:
- place: desktop
references:
- kind: code
  role: implementation
  target: src/kikoe/ui/transcription_controller.py#TranscriptionController.on_cancel_import
- kind: code
  role: implementation
  target: src/kikoe/services/importer.py
- kind: code
  role: implementation
  target: src/kikoe/services/file_transcription.py
- kind: code
  role: implementation
  target: src/kikoe/services/commits.py
domain: notes
---

# Cancel transcription

Abandon conversion or file transcription before its final save; wait for cleanup before allowing new work.
