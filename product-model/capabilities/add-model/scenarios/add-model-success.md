---
kind: primary
routes:
  desktop: Desktop
steps:
- text: Submit the identifier, display name and supported options.
  kind: actor
  entities: []
  contexts:
    desktop:
      place: desktop::provider
  actor: user
- text: Save the model with supported options and a display name defaulting to its identifier.
  kind: product
  entities:
  - entity: model
    effect: creates
    facts:
    - Model ID
    - Display name
    - File support
    - Realtime support
  contexts:
    desktop:
      place: desktop::provider
  actor: user
references:
- kind: code
  role: implementation
  target: src/kikoe/ui/model_dialog.py
- kind: code
  role: implementation
  target: src/kikoe/storage/providers.py#ProviderRepository.save_model
- kind: code
  role: implementation
  target: src/kikoe/core/model_catalog.py
---

# Add a model to a provider

## Trigger

The user enters a model ID in Add Model on a saved provider and chooses Add.

## Outcome

The model is listed under its provider and offered in the transcription picker; a blank display name shows the model ID.

## Edge cases

- The model ID must be nonempty and unique within its provider, and at least one mode must stay on.
- Typing a known model ID applies its preset until an option is changed by hand.
- Unsaved changes require a discard decision on dismissal; Cancel discards immediately.
- A model ID added meanwhile is reported as a duplicate without overwriting that definition.
