---
entities:
- entity: note
  shows:
  - Title
  - Created
  - Recordings
  - Duration
  - Display options
  collects:
  - Title
  - Display options
- entity: recording
  shows:
  - Created
  - Source
  - Duration
  - Original audio
  - Provider and model
  - Transcript
  - Timestamps
  - Speaker assignments
  collects:
  - Transcript
  - Timestamps
  - Speaker assignments
- entity: speaker
  shows:
  - Name
  - Number
  collects:
  - Name
- entity: microphone-capture
  shows:
  - Elapsed
  - Model and options
  - Confirmed text
  - Connection
references:
- kind: code
  role: implementation
  target: src/kikoe/ui/note_view.py
- kind: code
  role: implementation
  target: src/kikoe/ui/window.py
- kind: code
  role: implementation
  target: src/kikoe/ui/speaker_dialog.py
- kind: code
  role: implementation
  target: src/kikoe/ui/export_dialog.py
---

# Note

Review one note and its audio sections, capture or import audio, refine passages and speakers, and export the result. Capture, recovery results, speaker matching and export decisions stay within this subject.
