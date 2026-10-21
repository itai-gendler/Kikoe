---
kind: primary
routes:
  desktop: Desktop
steps:
- text: Confirm removal of one recording.
  kind: actor
  entities:
  - entity: recording
    effect: reads
    facts: []
  contexts:
    desktop:
      place: desktop::note
  actor: user
- text: Remove the recording and refresh the containing note duration and ordered recordings.
  kind: product
  entities:
  - entity: recording
    effect: removes
    from: Ready
  - entity: note
    effect: changes
    facts:
    - Recordings
    - Duration
  contexts:
    desktop:
      place: desktop::note
  actor: user
references:
- kind: code
  role: implementation
  target: src/kikoe/ui/note_actions.py#NoteActions.on_delete_recording
- kind: code
  role: implementation
  target: src/kikoe/storage/library.py#Library.delete_recording
---

# Delete recording

## Trigger

The user chooses Delete Recording and confirms.

## Outcome

The recording, its text and its original audio are deleted; the note keeps its other recordings and its duration is updated.

## Edge cases

- The final recording may be removed, leaving an empty note.
- Pending or incomplete items can also be deleted.
- Cancelling confirmation leaves the audio section intact.
