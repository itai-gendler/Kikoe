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
    effect: changes
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

# Save changes to a model

## Trigger

The user changes a model in Edit Model and saves.

## Outcome

The model keeps its place under its provider with the new ID, name and supported options.

## Edge cases

- The model ID must stay nonempty and unique within its provider, and at least one mode must stay on.
- Saved choices are kept; presets do not replace them, and options the API cannot support stay off.
- Unsaved changes require a discard decision on dismissal; Cancel discards immediately.
- A model removed or duplicated meanwhile is reported without overwriting another definition.
