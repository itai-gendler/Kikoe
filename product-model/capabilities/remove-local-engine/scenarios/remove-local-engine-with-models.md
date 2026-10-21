---
kind: alternate
routes:
  desktop: Desktop
steps:
- text: Confirm removal of the local engine and local model files.
  kind: actor
  entities:
  - entity: local-engine
    effect: reads
    facts: []
  - entity: local-model
    effect: reads
    facts: []
  contexts:
    desktop:
      place: desktop::local-models
  actor: user
- text: Remove the local engine and each installed local model.
  kind: product
  entities:
  - entity: local-engine
    effect: changes
    facts:
    - Readiness
    from: Installed
    to: Not downloaded
  - entity: local-model
    effect: changes
    facts:
    - Engine availability
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
  target: src/kikoe/ui/local_engine_group.py#LocalEngineGroup._on_remove_response
- kind: code
  role: implementation
  target: src/kikoe/services/local_models.py#LocalModelManager.remove_engine
---

# Remove an engine and its models

## Trigger

The user explicitly confirms removal including downloaded models.

## Outcome

The engine and its model files are no longer installed.
