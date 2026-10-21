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
  target: src/kikoe/core/upload.py
- kind: code
  role: implementation
  target: src/kikoe/services/importer.py
- kind: code
  role: implementation
  target: src/kikoe/services/upload_queue.py
---

# Chunk completion order never changes transcript order

Long audio is split at pauses into parts within the provider’s chunk limits, and each converted part is checked again before it is sent. Completed text and timestamps follow source order whatever order the parts finish in, and the streaming preview shows only the finished beginning. Simultaneous jobs on one provider share its Parallel Requests.
