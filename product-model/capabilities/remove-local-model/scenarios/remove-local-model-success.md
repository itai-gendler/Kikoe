---
kind: primary
routes:
  desktop: Desktop
steps:
- text: Confirm local model removal.
  kind: actor
  entities:
  - entity: local-model
    effect: reads
    facts: []
  contexts:
    desktop:
      place: desktop::local-models
  actor: user
- text: Remove the local model file and refresh available transcription choices.
  kind: product
  entities:
  - entity: local-model
    effect: changes
    facts:
    - Download progress
    from: Installed
    to: Not downloaded
  contexts:
    desktop:
      place: desktop::local-models
  actor: user
references:
- kind: code
  role: implementation
  target: src/kikoe/ui/local_model_list.py#LocalModelList._confirm_removal
- kind: code
  role: implementation
  target: src/kikoe/services/local_models.py#LocalModelManager.remove_model
---

# Remove local model

## Trigger

The user removes a downloaded model and confirms.

## Outcome

The model file is deleted and the model is no longer offered On This Device; it can be downloaded again.

## Edge cases

- Removing a supplemental speaker model removes the extra speaker option from dependent local speech models.
