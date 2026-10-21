---
availability:
- place: desktop
references:
- kind: code
  role: implementation
  target: src/kikoe/ui/bottom_bar.py
- kind: code
  role: implementation
  target: src/kikoe/ui/transcription_dialog.py
- kind: code
  role: implementation
  target: src/kikoe/core/choice.py
---

# Choose model

Choose the next transcription model and request timestamps and speakers according to its mode support. The recent model survives restart; in-window feature requests survive selecting a model without those features.
