---
kind: primary
routes:
  desktop: Desktop
steps:
- text: Inspect the available local components.
  kind: actor
  entities: []
  contexts:
    desktop:
      place: desktop::local-models
  actor: user
- text: Show each local engine readiness and each local model installation and engine availability.
  kind: product
  entities:
  - entity: local-engine
    effect: reads
    facts:
    - Name
    - Version
    - Acceleration
    - Device
    - Download progress
    - Readiness
    - Included with Kikoe
  - entity: local-model
    effect: reads
    facts:
    - Name
    - Size
    - Languages
    - Features
    - Purpose
    - Download progress
    - Engine availability
  contexts:
    desktop:
      place: desktop::local-models
  actor: user
references:
- kind: code
  role: implementation
  target: src/kikoe/ui/local_models_page.py
- kind: code
  role: implementation
  target: src/kikoe/ui/local_engine_group.py
- kind: code
  role: implementation
  target: src/kikoe/ui/local_model_list.py
- kind: code
  role: implementation
  target: src/kikoe/services/local_models.py
---

# Browse local models

## Trigger

The user opens Preferences → Local Models.

## Outcome

Each engine shows its version, readiness and devices, and each model its size, languages, features and whether it is downloaded.

## Edge cases

- Unsupported platforms show that no engine builds are available.
- An engine startup failure is explained and no device list is offered until probing succeeds.
- Installed models whose engine is absent remain listed as needing that engine.
