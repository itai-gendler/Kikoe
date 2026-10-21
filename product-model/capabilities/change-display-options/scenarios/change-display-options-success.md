---
kind: primary
routes:
  desktop: Desktop
steps:
- text: Change the note display options.
  kind: actor
  entities:
  - entity: note
    effect: reads
    facts: []
  contexts:
    desktop:
      place: desktop::note
  actor: user
- text: Save note display options without altering recording transcript, timing or identities.
  kind: product
  entities:
  - entity: note
    effect: changes
    facts:
    - Display options
  - entity: recording
    effect: reads
    facts:
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
  target: src/kikoe/ui/display_actions.py
- kind: code
  role: implementation
  target: src/kikoe/core/export.py
---

# Change display options

## Trigger

The user turns Show Timestamps or Show Speakers on or off for a note.

## Outcome

The note’s display options are saved; stored times and speakers are unchanged, and later copies and exports start from these options.
