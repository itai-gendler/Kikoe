---
kind: primary
routes:
  desktop: Desktop
steps:
- text: Apply changed provider details.
  kind: actor
  entities:
  - entity: provider
    effect: reads
    facts: []
  contexts:
    desktop:
      place: desktop::provider
  actor: user
- text: Save provider fields and re-evaluate its model definitions against the selected API limits.
  kind: product
  entities:
  - entity: provider
    effect: changes
    facts:
    - Name
    - API type
    - Base URL
    - API key
    - Upload settings
    - Audio LLM settings
  - entity: model
    effect: changes
    facts:
    - File support
    - Realtime support
  contexts:
    desktop:
      place: desktop::provider
  actor: user
references:
- kind: code
  role: implementation
  target: src/kikoe/ui/provider_page.py
- kind: code
  role: implementation
  target: src/kikoe/storage/providers.py
---

# Edit provider

## Trigger

The user changes a saved provider’s field and confirms it, or changes its API type or an upload setting.

## Outcome

The change is saved at once and its models are kept within what the API supports; work already running keeps the settings it started with.

## Edge cases

- Changing API type resets upload and Audio LLM settings to defaults.
- Audio LLM prompt edits save when leaving the text field or closing the page.
- A blank prompt uses the built-in transcription prompt.
- Upload settings apply immediately and running jobs keep their original snapshot.
- Invalid connection fields are not saved.
