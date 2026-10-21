---
kind: primary
result: achieved
routes:
  desktop: Desktop
steps:
- text: Choose Recover for the unfinished sessions.
  kind: actor
  entities: []
  contexts:
    desktop:
      place: desktop
  actor: user
  capability: recover-recordings
- text: Finalize microphone capture audio and add a pending recording to the note.
  kind: product
  entities:
  - entity: microphone-capture
    effect: removes
    from: Interrupted
  - entity: recording
    effect: creates
    facts:
    - Created
    - Source
    - Duration
    - Original audio
    - Provider and model
    - Transcript
    - Timestamps
    - Speaker assignments
    to: Pending
  - entity: note
    effect: changes
    facts:
    - Recordings
    - Duration
  contexts:
    desktop:
      place: desktop
  actor: user
  capability: recover-recordings
- text: Open the recovered note and recording for review or explicit retry.
  kind: product
  entities:
  - entity: note
    effect: reads
    facts:
    - Title
    - Created
    - Recordings
    - Duration
    - Display options
  - entity: recording
    effect: reads
    facts:
    - Created
    - Source
    - Duration
    - Original audio
    - Provider and model
    - Transcript
    - Timestamps
    - Speaker assignments
  contexts:
    desktop:
      place: desktop::note
  actor: user
  capability: recover-recordings
- text: Retry transcription.
  kind: actor
  entities: []
  contexts:
    desktop:
      place: desktop::note
  actor: user
  capability: retry-transcription
- text: Complete the pending recording using the selected file model.
  kind: product
  entities:
  - entity: recording
    effect: changes
    facts:
    - Transcript
    - Timestamps
    - Speaker assignments
    - Provider and model
    from: Pending
    to: Ready
  - entity: model
    effect: reads
    facts: []
  contexts:
    desktop:
      place: desktop::note
  actor: user
  capability: retry-transcription
references:
- kind: code
  role: implementation
  target: src/kikoe/ui/recording_controller.py#RecordingController._show_recovered_note
- kind: code
  role: implementation
  target: src/kikoe/ui/transcription_controller.py#TranscriptionController._retry
---

# Transcribe a recovered note

## Trigger

The user restores interrupted microphone audio.

## Outcome

The recovered note opens and its retained recording is explicitly transcribed with a file model.
