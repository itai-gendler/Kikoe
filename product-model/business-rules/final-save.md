---
appliesTo:
- type: capability
  id: cancel-transcription
- type: capability
  id: close-kikoe
- type: capability
  id: stop-recording
- type: capability
  id: recover-recordings
references:
- kind: code
  role: implementation
  target: src/kikoe/core/activity.py#Stage
- kind: code
  role: implementation
  target: src/kikoe/services/commits.py
- kind: code
  role: implementation
  target: src/kikoe/services/activity.py
---

# Final saving completes before cancellation or close

Cancellation is available only while converting or transcribing. Stopping capture, saving audio, recovering audio and final transcript saving finish rather than being cancelled. Close waits for pending edits and submitted final writes.
