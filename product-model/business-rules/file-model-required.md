---
appliesTo:
- type: capability
  id: import-audio
- type: capability
  id: retry-transcription
- type: capability
  id: retranscribe-recording
- type: capability
  id: start-recording
references:
- kind: code
  role: implementation
  target: src/kikoe/core/activity.py#action_availability
- kind: code
  role: implementation
  target: src/kikoe/services/importer.py
- kind: code
  role: implementation
  target: src/kikoe/services/file_transcription.py
---

# File operations require file model support

Import, retry and re-transcription require a file-capable model. Live-only choices are never silently replaced. Microphone capture prefers realtime whenever the selected model supports it.
