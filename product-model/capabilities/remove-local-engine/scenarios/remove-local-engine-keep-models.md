---
kind: primary
routes:
  desktop: Desktop
steps:
- text: Confirm local engine removal.
  kind: actor
  entities:
  - entity: local-engine
    effect: reads
    facts: []
  contexts:
    desktop:
      place: desktop::local-models
  actor: user
- text: Remove the local engine installation and refresh local model availability.
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

# Remove an engine but keep models

## Trigger

The user confirms Remove Engine.

## Outcome

Models remain downloaded but cannot be used until the engine is installed again.
