---
appliesTo:
- type: capability
  id: pause-recording
- type: capability
  id: resume-recording
- type: capability
  id: stop-recording
references:
- kind: code
  role: implementation
  target: src/kikoe/services/recording.py
- kind: code
  role: implementation
  target: src/kikoe/services/realtime.py
---

# Paused time is excluded from recorded audio and duration

Pause and resume operate on the same capture. Elapsed duration follows accepted samples, and live recognition resumes from confirmed audio with a separate recognition scope.
