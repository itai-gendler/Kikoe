---
entities:
- entity: preferences
  shows:
  - Language
  - Custom vocabulary
  - Live transcription delay
  - Microphone
  - Audio output
  - Data folder
  - Log folder
  collects:
  - Language
  - Custom vocabulary
  - Live transcription delay
  - Microphone
  - Audio output
references:
- kind: code
  role: implementation
  target: src/kikoe/ui/preferences.py
---

# General

Set transcription and audio defaults and reach local data and logs.
