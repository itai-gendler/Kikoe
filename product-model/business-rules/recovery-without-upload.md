---
appliesTo:
- type: entity
  id: microphone-capture
- type: entity
  id: recording
references:
- kind: code
  role: implementation
  target: src/kikoe/services/recovery.py
---

# Recovery never uploads automatically

Recovery restores accepted audio and confirmed text as pending transcription. It recognizes already saved recordings to avoid duplicates, and recreates the destination note when it no longer exists. Transcription resumes only after the user explicitly retries.
