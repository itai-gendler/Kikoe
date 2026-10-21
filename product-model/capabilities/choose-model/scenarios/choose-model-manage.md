---
kind: alternate
routes:
  desktop: Desktop
steps:
- text: Choose Manage Providers and Models from the transcription picker.
  kind: actor
  actor: user
  entities:
  - entity: provider
    effect: reads
    facts: []
  - entity: model
    effect: reads
    facts: []
  contexts:
    desktop:
      place: desktop::transcription-model
- text: Close the picker and open Providers in Preferences.
  kind: product
  actor: user
  entities:
  - entity: provider
    effect: reads
    facts: []
  - entity: preferences
    effect: reads
    facts: []
  contexts:
    desktop:
      place: desktop::providers
references:
- kind: code
  role: implementation
  target: src/kikoe/ui/transcription_dialog.py#TranscriptionDialog._on_manage_row_activated
- kind: code
  role: implementation
  target: src/kikoe/application.py#Application._present_preferences
---

# Open configuration from the transcription picker

## Trigger

The user needs to add or change available transcription choices.

## Outcome

The picker closes and Preferences opens to Providers, where connections and model definitions can be configured.
