---
kind: edge
routes:
  desktop: Desktop
steps:
- text: Download the local engine.
  kind: actor
  entities:
  - entity: local-engine
    effect: reads
    facts: []
  contexts:
    desktop:
      place: desktop::local-models
  actor: user
- text: Begin local engine download.
  kind: product
  entities:
  - entity: local-engine
    effect: changes
    facts:
    - Download progress
    from: Not downloaded
    to: Downloading
  contexts:
    desktop:
      place: desktop::local-models
  actor: user
- text: Report the failure and leave the local engine not downloaded.
  kind: product
  entities:
  - entity: local-engine
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
  target: src/kikoe/services/local_models.py#LocalModelManager.install_engine
- kind: code
  role: implementation
  target: src/kikoe/storage/local_installs.py
- kind: code
  role: implementation
  target: src/kikoe/ui/local_engine_group.py
---

# Report engine download failure

## Trigger

A download or installation fails.

## Outcome

No new engine installation is published and the error is shown.
