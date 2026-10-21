---
kind: primary
routes:
  desktop: Desktop
steps:
- text: Cancel the local engine download.
  kind: actor
  entities:
  - entity: local-engine
    effect: reads
    facts: []
  contexts:
    desktop:
      place: desktop::local-models
  actor: user
- text: Cancel downloading the local engine and release partial files.
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
  target: src/kikoe/services/local_models.py#LocalModelManager.cancel
- kind: code
  role: implementation
  target: src/kikoe/storage/local_installs.py
---

# Cancel a local engine download

## Trigger

The user chooses Cancel during a download.

## Outcome

The download ends and the engine is not installed.
