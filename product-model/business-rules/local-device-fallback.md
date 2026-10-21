---
appliesTo:
- type: entity
  id: preferences
  facts:
  - Microphone
  - Audio output
references:
- kind: code
  role: implementation
  target: src/kikoe/media/devices.py#resolve_device
- kind: code
  role: implementation
  target: src/kikoe/ui/preferences.py
---

# Unavailable saved audio devices fall back to System Default

Input and output choices are saved by name. A missing saved device stays visible as unavailable and sound uses the system default; running capture keeps the device with which it began.
