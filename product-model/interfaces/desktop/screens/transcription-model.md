---
entities:
- entity: preferences
  shows:
  - Recent model
  - Requested features
  collects:
  - Recent model
  - Requested features
- entity: provider
  shows:
  - Name
- entity: model
  shows:
  - Display name
  - File support
  - Realtime support
- entity: local-model
  shows:
  - Name
  - Features
references:
- kind: code
  role: implementation
  target: src/kikoe/ui/transcription_dialog.py
- kind: code
  role: implementation
  target: src/kikoe/ui/model_chooser_page.py
---

# Transcription Model

Choose a configured or installed local model and requested timestamps and speakers; search belongs to that choice.
