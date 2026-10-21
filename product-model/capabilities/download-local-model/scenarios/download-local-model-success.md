---
kind: primary
routes:
  desktop: Desktop
steps:
- text: Download the local model.
  kind: actor
  entities:
  - entity: local-model
    effect: reads
    facts: []
  contexts:
    desktop:
      place: desktop::local-models
  actor: user
- text: Download the local model with progress.
  kind: product
  entities:
  - entity: local-model
    effect: changes
    facts:
    - Download progress
    from: Not downloaded
    to: Downloading
  contexts:
    desktop:
      place: desktop::local-models
  actor: user
- text: Publish the installed local model and its engine availability.
  kind: product
  entities:
  - entity: local-model
    effect: changes
    facts:
    - Download progress
    - Engine availability
    from: Downloading
    to: Installed
  contexts:
    desktop:
      place: desktop::local-models
  actor: user
references:
- kind: code
  role: implementation
  target: src/kikoe/services/local_models.py#LocalModelManager.install_model
- kind: code
  role: implementation
  target: src/kikoe/ui/local_model_list.py
- kind: code
  role: implementation
  target: src/kikoe/storage/local_installs.py
---

# Install a local model

## Trigger

The user chooses Download for a catalog model.

## Outcome

The model file is installed; a usable speech model appears as On This Device in the transcription picker.

## Edge cases

- The speaker-detection model augments timestamp-capable speech models and is not a standalone transcription choice.
- Models may be downloaded before their engine.
