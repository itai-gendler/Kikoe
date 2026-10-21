---
kind: primary
routes:
  desktop: Desktop
steps:
- text: Switch the local engine acceleration build.
  kind: actor
  entities:
  - entity: local-engine
    effect: reads
    facts: []
  contexts:
    desktop:
      place: desktop::local-models
  actor: user
- text: Download the replacement local engine.
  kind: product
  entities:
  - entity: local-engine
    effect: changes
    facts:
    - Download progress
    from: Installed
    to: Downloading
  contexts:
    desktop:
      place: desktop::local-models
  actor: user
- text: Publish the replacement local engine and inspect its devices.
  kind: product
  entities:
  - entity: local-engine
    effect: changes
    facts:
    - Acceleration
    - Version
    - Readiness
    - Download progress
    from: Downloading
    to: Installed
  contexts:
    desktop:
      place: desktop::local-models
  actor: user
references:
- kind: code
  role: implementation
  target: src/kikoe/ui/local_engine_group.py
- kind: code
  role: implementation
  target: src/kikoe/services/local_models.py#LocalModelManager.install_engine
- kind: code
  role: implementation
  target: src/kikoe/storage/local_installs.py
---

# Replace an acceleration build

## Trigger

The user chooses another build and Switch.

## Outcome

The replacement engine is used after installation; local model downloads remain.

## Edge cases

- Failure or cancellation before replacement retains the prior installation.
