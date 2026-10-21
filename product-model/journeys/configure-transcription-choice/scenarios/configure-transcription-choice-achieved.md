---
kind: primary
result: achieved
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
  capability: choose-model
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
  capability: choose-model
- text: Choose a provider to inspect.
  kind: actor
  entities:
  - entity: provider
    effect: reads
    facts:
    - Name
    - API type
  contexts:
    desktop:
      place: desktop::providers
  actor: user
  capability: browse-providers
- text: Show provider connection fields and model definitions.
  kind: product
  entities:
  - entity: provider
    effect: reads
    facts:
    - Name
    - API type
    - Base URL
    - API key
    - Upload settings
    - Audio LLM settings
  - entity: model
    effect: reads
    facts:
    - Model ID
    - Display name
    - File support
    - Realtime support
  contexts:
    desktop:
      place: desktop::provider
  actor: user
  capability: browse-providers
references:
- kind: code
  role: implementation
  target: src/kikoe/ui/transcription_dialog.py#TranscriptionDialog._on_manage_row_activated
- kind: code
  role: implementation
  target: src/kikoe/application.py#Application._present_preferences
---

# Configure a transcription choice

## Trigger

The user opens management from the transcription picker.

## Outcome

The configured connection is open for editing after Kikoe carries the user into Preferences.
