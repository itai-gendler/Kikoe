---
availability:
- place: desktop
references:
- kind: code
  role: implementation
  target: src/kikoe/ui/window.py#Window._save_and_close
- kind: code
  role: implementation
  target: src/kikoe/services/activity.py#ActivityTracker.wind_down
- kind: code
  role: implementation
  target: src/kikoe/services/recording_workflow.py
---

# Close Kikoe

Close or quit while preserving accepted microphone audio and waiting for pending edits and final saves.
