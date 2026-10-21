---
kind: primary
routes:
  desktop: Desktop
steps:
- text: Copy all note text.
  kind: actor
  entities:
  - entity: note
    effect: reads
    facts: []
  contexts:
    desktop:
      place: desktop::note
  actor: user
- text: Wait for pending edits and copy the note and recording passages with resolved speaker names to
    the clipboard.
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
references:
- kind: code
  role: implementation
  target: src/kikoe/ui/export_controller.py#ExportController._copy_all_text
- kind: code
  role: implementation
  target: src/kikoe/core/export.py
---

# Copy all text

## Trigger

The user chooses Copy All Text from the note menu.

## Outcome

Once pending edits are saved, the clipboard holds the note’s text, with times and speaker names as the note’s display options show them.
