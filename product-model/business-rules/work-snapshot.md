---
appliesTo:
- type: capability
  id: choose-model
- type: capability
  id: edit-provider
- type: capability
  id: change-general-settings
- type: capability
  id: start-recording
- type: capability
  id: import-audio
- type: capability
  id: retry-transcription
- type: capability
  id: retranscribe-recording
references:
- kind: code
  role: implementation
  target: src/kikoe/ui/transcription_controller.py
- kind: code
  role: implementation
  target: src/kikoe/ui/recording_controller.py
- kind: code
  role: implementation
  target: src/kikoe/services/importer.py
---

# Running transcription keeps its starting choices

Model, provider upload settings, language and requested transcription features are captured at job start. Changed preferences apply to later work.
