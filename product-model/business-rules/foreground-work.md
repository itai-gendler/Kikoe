---
appliesTo:
- type: capability
  id: start-recording
- type: capability
  id: import-audio
- type: capability
  id: retry-transcription
- type: capability
  id: retranscribe-recording
- type: capability
  id: browse-notes
- type: capability
  id: edit-transcript
- type: capability
  id: delete-note
- type: capability
  id: delete-recording
- type: capability
  id: export-note
- type: capability
  id: play-recording
- type: capability
  id: rename-note
- type: capability
  id: rename-speaker
- type: capability
  id: match-speakers
references:
- kind: code
  role: implementation
  target: src/kikoe/core/activity.py
- kind: code
  role: implementation
  target: src/kikoe/ui/window.py#Window.refresh_actions
---

# Conflicting work waits for the active task

Only one foreground recording or file-transcription task runs in a window. Capture and recovery keep the selected note fixed. File transcription allows opening another note, while edits, playback, deletion, rename and export on its target wait for the task; search and sidebar rename/delete remain unavailable while busy. Display options remain usable.
