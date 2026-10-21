---
kind: primary
result: achieved
routes:
  desktop: Desktop
steps:
- text: Enter and submit a nonempty title.
  kind: actor
  entities: []
  contexts:
    desktop:
      place: desktop::notes
  actor: user
  capability: create-note
- text: Create the empty note with its trimmed title, creation time, zero duration and both display options
    on.
  kind: product
  entities:
  - entity: note
    effect: creates
    facts:
    - Title
    - Created
    - Recordings
    - Duration
    - Display options
  contexts:
    desktop:
      place: desktop::notes
  actor: user
  capability: create-note
- text: Open the new note.
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
  contexts:
    desktop:
      place: desktop::note
  actor: user
  capability: create-note
- text: Start the microphone for the note.
  kind: actor
  entities:
  - entity: note
    effect: reads
    facts:
    - Title
  contexts:
    desktop:
      place: desktop::note
  actor: user
  capability: start-recording
- text: Open the microphone and begin a microphone capture with the selected model and options.
  kind: product
  entities:
  - entity: microphone-capture
    effect: creates
    facts:
    - Destination
    - Started
    - Audio
    - Elapsed
    - Model and options
    - Confirmed text
    - Connection
    to: Recording
  - entity: preferences
    effect: reads
    facts:
    - Recent model
    - Requested features
    - Language
    - Custom vocabulary
    - Live transcription delay
    - Microphone
  - entity: model
    effect: reads
    facts: []
  contexts:
    desktop:
      place: desktop::note
  actor: user
  capability: start-recording
- text: Retain accepted sound and confirmed text in the microphone capture while showing connection progress.
  kind: product
  entities:
  - entity: microphone-capture
    effect: changes
    facts:
    - Audio
    - Elapsed
    - Confirmed text
    - Connection
  contexts:
    desktop:
      place: desktop::note
  actor: user
  capability: start-recording
- text: Stop microphone capture.
  kind: actor
  entities:
  - entity: microphone-capture
    effect: reads
    facts: []
  contexts:
    desktop:
      place: desktop::note
  actor: user
  capability: stop-recording
- text: End microphone capture and finish accepted audio.
  kind: product
  entities:
  - entity: microphone-capture
    effect: changes
    facts:
    - Audio
    - Elapsed
    from: Recording
    to: Stopped
  contexts:
    desktop:
      place: desktop::note
  actor: user
  capability: stop-recording
- text: Save a recording with retained audio and confirmed text, and release the microphone capture.
  kind: product
  entities:
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
  - entity: microphone-capture
    effect: removes
    from: Stopped
  - entity: note
    effect: changes
    facts:
    - Recordings
    - Duration
  contexts:
    desktop:
      place: desktop::note
  actor: user
  capability: stop-recording
- text: Finish the recording with complete transcription.
  kind: product
  entities:
  - entity: recording
    effect: changes
    facts:
    - Transcript
    - Timestamps
    - Speaker assignments
    from: Pending
    to: Ready
  contexts:
    desktop:
      place: desktop::note
  actor: user
  capability: stop-recording
references:
- kind: code
  role: implementation
  target: src/kikoe/ui/note_actions.py#NoteActions._create_note
- kind: code
  role: implementation
  target: src/kikoe/ui/recording_controller.py
---

# Capture in a named note

## Trigger

The user creates a note with a chosen title.

## Outcome

The named note contains retained audio and the complete live transcript after capture is stopped.
