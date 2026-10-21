---
availability:
- place: desktop
references:
- kind: code
  role: implementation
  target: src/kikoe/ui/transcription_controller.py#TranscriptionController._retry
- kind: code
  role: implementation
  target: src/kikoe/services/file_transcription.py#FileTranscriptionWorkflow.transcribe_pending
domain: notes
---

# Retry transcription

Use the current file model and options to transcribe retained pending or incomplete audio in place.
