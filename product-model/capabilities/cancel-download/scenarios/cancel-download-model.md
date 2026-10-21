---
kind: alternate
routes:
  desktop: Desktop
steps:
- text: Cancel the local model download.
  kind: actor
  entities:
  - entity: local-model
    effect: reads
    facts: []
  contexts:
    desktop:
      place: desktop::local-models
  actor: user
- text: Cancel downloading the local model and release partial files.
  kind: product
  entities:
  - entity: local-model
    effect: changes
    facts:
    - Download progress
    from: Downloading
    to: Not downloaded
  contexts:
    desktop:
      place: desktop::local-models
  actor: user
references:
- kind: code
  role: implementation
  target: src/kikoe/services/local_models.py#LocalModelManager.cancel
- kind: code
  role: implementation
  target: src/kikoe/storage/local_installs.py
---

# Cancel a local model download

## Trigger

The user chooses Cancel during a download.

## Outcome

The download ends and the model is not installed.
