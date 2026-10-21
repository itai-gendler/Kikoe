---
kind: alternate
routes:
  desktop: Desktop
steps:
- text: Cancel replacement of the local engine.
  kind: actor
  actor: user
  entities:
  - entity: local-engine
    effect: reads
    facts:
    - Acceleration
  contexts:
    desktop:
      place: desktop::local-models
- text: Keep the previously installed local engine after releasing the partial download.
  kind: product
  actor: user
  entities:
  - entity: local-engine
    effect: changes
    from: Downloading
    to: Installed
    facts:
    - Download progress
    - Readiness
  contexts:
    desktop:
      place: desktop::local-models
references:
- kind: code
  role: implementation
  target: src/kikoe/storage/local_installs.py#LocalInstalls.install_engine
- kind: code
  role: implementation
  target: src/kikoe/services/local_models.py#LocalModelManager._state
---

# Cancel an acceleration switch

## Trigger

A replacement build is downloading and the user cancels before replacement.

## Outcome

The previous engine installation remains available with its model files.
