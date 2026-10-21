---
appliesTo:
- type: capability
  id: import-audio
- type: capability
  id: retry-transcription
- type: capability
  id: retranscribe-recording
references:
- kind: code
  role: implementation
  target: src/kikoe/services/importer.py
- kind: code
  role: implementation
  target: src/kikoe/providers/chat_file_stream.py
- kind: code
  role: implementation
  target: src/kikoe/storage/library.py#Library.update_transcription
---

# Only complete file results replace saved text

All chunks must succeed before transcript changes commit. Temporary streaming text is not saved as a completed result. A successful empty response can be a complete result; an output-limit or content-filter finish is a failure.
