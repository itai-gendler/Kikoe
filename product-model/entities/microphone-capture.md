---
domain: notes
references:
- kind: code
  role: implementation
  target: src/kikoe/services/recording.py#RecordingSession
- kind: code
  role: implementation
  target: src/kikoe/services/realtime.py#RealtimeRecording
- kind: code
  role: implementation
  target: src/kikoe/storage/captures.py
---

# Microphone capture

The current or interrupted microphone session, before its retained recording has been finalized.

## Information kept

- **Destination** — The note receiving audio and its title for recovery.
- **Started** — When capture began.
- **Audio** — Accepted microphone sound, retained incrementally.
- **Elapsed** — Duration of accepted sound; paused time is excluded.
- **Model and options** — The active session’s selected model, requested features and language; recovery retains provider and model attribution.
- **Confirmed text** — Recognition results already confirmed; provisional live text is separate.
- **Connection** — Preparing, live, reconnecting, catching up, paused or incomplete recognition.

## States

### Recording

The microphone accepts sound.

### Paused

Capture is paused within the same session.

### Stopped

Capture has ended and local finalization is in progress.

### Interrupted

An unfinished session is available for recovery after interruption.
