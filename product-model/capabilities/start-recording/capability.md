---
availability:
- place: desktop
references:
- kind: code
  role: implementation
  target: src/kikoe/services/recording_workflow.py
- kind: code
  role: implementation
  target: src/kikoe/services/recording.py
- kind: code
  role: implementation
  target: src/kikoe/services/realtime.py
domain: notes
---

# Start recording

Start or append microphone capture using the chosen model. Live-capable models transcribe during capture; file-only models transcribe retained audio after Stop.
