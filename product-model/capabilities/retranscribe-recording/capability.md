---
availability:
- place: desktop
references:
- kind: code
  role: implementation
  target: src/kikoe/ui/retranscribe_dialog.py
- kind: code
  role: implementation
  target: src/kikoe/services/file_transcription.py#FileTranscriptionWorkflow.retranscribe
- kind: code
  role: implementation
  target: src/kikoe/storage/library.py#Library.update_transcription
domain: notes
---

# Re-transcribe recording

Replace the transcript of retained audio using a file model chosen for this run. Successful replacement includes manual edits; neighboring recordings stay intact.
