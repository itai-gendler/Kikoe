---
kind: primary
routes:
  desktop: Desktop
steps:
- text: Search available model choices.
  kind: actor
  entities:
  - entity: model
    effect: reads
    facts:
    - Display name
    - File support
    - Realtime support
  - entity: local-model
    effect: reads
    facts:
    - Name
    - Features
  - entity: provider
    effect: reads
    facts:
    - Name
  contexts:
    desktop:
      place: desktop::transcription-model
  actor: user
- text: Choose a model and requested features.
  kind: actor
  entities:
  - entity: model
    effect: reads
    facts: []
  contexts:
    desktop:
      place: desktop::transcription-model
  actor: user
- text: Save the recent choice in preferences and keep the current window feature requests.
  kind: product
  entities:
  - entity: preferences
    effect: changes
    facts:
    - Recent model
    - Requested features
  contexts:
    desktop:
      place: desktop::transcription-model
  actor: user
references:
- kind: code
  role: implementation
  target: src/kikoe/ui/bottom_bar.py
- kind: code
  role: implementation
  target: src/kikoe/ui/transcription_dialog.py
- kind: code
  role: implementation
  target: src/kikoe/core/choice.py
---

# Choose a model and options

## Trigger

The user opens Transcription Model.

## Outcome

The selected model and requested options apply to subsequent work; running work retains its starting choices.

## Edge cases

- Every search word must appear in the model display name, model ID or provider name, ignoring case.
- Unsupported feature switches are unavailable; remembered requests return with a supporting model.
- A missing recent choice falls back to the first available model.
- File-only requests use file capabilities even when capture would use realtime capabilities.
