---
kind: edge
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
- text: Begin the local model download.
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
- text: Report failure and return the local model to not downloaded.
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
  target: src/kikoe/services/local_models.py#LocalModelManager.install_model
- kind: code
  role: implementation
  target: src/kikoe/ui/local_model_list.py
- kind: code
  role: implementation
  target: src/kikoe/storage/local_installs.py
---

# Report model download failure

## Trigger

The local model download or installation fails.

## Outcome

No completed model installation is offered.
