---
kind: primary
routes:
  desktop: Desktop
steps:
- text: Export the note as text or Markdown.
  kind: actor
  entities:
  - entity: note
    effect: reads
    facts:
    - Title
    - Display options
  contexts:
    desktop:
      place: desktop::note
  actor: user
- text: Wait for pending edits, then render note text and recording passages with resolved speaker names.
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
  - entity: speaker
    effect: reads
    facts:
    - Name
    - Number
  contexts:
    desktop:
      place: desktop::note
  actor: user
- text: Choose a save location.
  kind: actor
  entities: []
  contexts:
    desktop:
      place: desktop::note
  actor: user
- text: Write the exported content and report success.
  kind: product
  entities: []
  contexts:
    desktop:
      place: desktop::note
  actor: user
references:
- kind: code
  role: implementation
  target: src/kikoe/ui/export_controller.py
- kind: code
  role: implementation
  target: src/kikoe/ui/export_dialog.py
- kind: code
  role: implementation
  target: src/kikoe/core/export.py
---

# Export text or Markdown

## Trigger

The user chooses a prose format and export options.

## Outcome

The chosen destination receives the current note, with optional times and speaker names and separate headings for multiple recordings.

## Edge cases

- Cancelling the save picker writes nothing.
- Write failures are explained and leave the library intact.
