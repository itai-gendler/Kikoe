---
kind: primary
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
references:
- kind: code
  role: implementation
  target: src/kikoe/ui/recording_controller.py#RecordingController.offer_recovery
- kind: code
  role: implementation
  target: src/kikoe/services/recovery.py
---

# Recover an interrupted capture

## Trigger

Startup finds unfinished microphone sessions and the user chooses Recover.

## Outcome

Retained audio and confirmed text become a pending recording in its note, which is opened.

## Edge cases

- An already saved capture is recognized and not duplicated.
- A zero-length capture is discarded without adding a recording.
- Conversion failure leaves recovery material for a later attempt.
