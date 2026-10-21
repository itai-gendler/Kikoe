---
actors:
- user
references:
- kind: code
  role: implementation
  target: src/kikoe/ui/recording_controller.py#RecordingController._show_recovered_note
- kind: code
  role: implementation
  target: src/kikoe/ui/transcription_controller.py#TranscriptionController._retry
---

# Transcribe a recovered note

## Goal

The user restores interrupted microphone audio.

## Success criterion

The recovered note opens and its retained recording is explicitly transcribed with a file model.
