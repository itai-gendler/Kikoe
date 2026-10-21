---
kind: primary
routes:
  desktop: Desktop
steps:
- text: Remove the model definition.
  kind: actor
  entities:
  - entity: model
    effect: reads
    facts: []
  contexts:
    desktop:
      place: desktop::provider
  actor: user
- text: Remove the model from available choices.
  kind: product
  entities:
  - entity: model
    effect: removes
  contexts:
    desktop:
      place: desktop::provider
  actor: user
references:
- kind: code
  role: implementation
  target: src/kikoe/ui/model_dialog.py#ModelDialog._remove
- kind: code
  role: implementation
  target: src/kikoe/storage/providers.py#ProviderRepository.remove_model
---

# Remove model

## Trigger

The user removes a model from its provider.

## Outcome

The model is no longer offered for new work; recordings made with it keep its name.
