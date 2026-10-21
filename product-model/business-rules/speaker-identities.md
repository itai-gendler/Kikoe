---
appliesTo:
- type: entity
  id: speaker
- type: entity
  id: recording
references:
- kind: code
  role: implementation
  target: src/kikoe/core/speakers.py
- kind: code
  role: implementation
  target: src/kikoe/core/transcription.py#scope_speakers
- kind: code
  role: implementation
  target: src/kikoe/storage/library.py#Library._replace_bindings
---

# Independent recognition labels do not establish the same person

Speaker numbers from separate recordings, chunks or connections remain separate identities until matched. Matching can combine labels and later restore their original identities. Re-transcription inherits an identity only with at least 80 percent timed overlap, a strictly better score than the runner-up and at least twice that score; uncertain matches need a decision.
