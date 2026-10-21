---
actors:
- user
references:
- kind: code
  role: implementation
  target: src/kikoe/ui/transcription_dialog.py#TranscriptionDialog._on_manage_row_activated
- kind: code
  role: implementation
  target: src/kikoe/application.py#Application._present_preferences
---

# Configure a transcription choice

## Goal

Reach configuration while choosing how to transcribe.

## Success criterion

The user is carried from the transcription picker into Providers and opens an existing connection for configuration.
