---
appliesTo:
- type: capability
  id: import-audio
- type: capability
  id: stop-recording
- type: capability
  id: retry-transcription
- type: capability
  id: retranscribe-recording
- type: capability
  id: export-note
references:
- kind: code
  role: implementation
  target: src/kikoe/services/importer.py
- kind: code
  role: implementation
  target: src/kikoe/services/file_transcription.py
- kind: code
  role: implementation
  target: src/kikoe/services/recording_workflow.py
---

# Retained originals survive transcription failure

Import copies are retained only with a successful import. Microphone audio is retained before file transcription; retries and replacement never remove that original on failure. Upload conversion does not change retained originals.
