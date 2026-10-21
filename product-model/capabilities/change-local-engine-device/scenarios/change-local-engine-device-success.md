---
kind: primary
routes:
  desktop: Desktop
steps:
- text: Choose a reported local engine device or Automatic.
  kind: actor
  entities:
  - entity: local-engine
    effect: reads
    facts: []
  contexts:
    desktop:
      place: desktop::local-models
  actor: user
- text: Save the local engine device preference for subsequent inference.
  kind: product
  entities:
  - entity: local-engine
    effect: changes
    facts:
    - Device
  contexts:
    desktop:
      place: desktop::local-models
  actor: user
references:
- kind: code
  role: implementation
  target: src/kikoe/ui/local_engine_group.py#LocalEngineGroup._on_device_row_notify_selected
- kind: code
  role: implementation
  target: src/kikoe/services/local_models.py#LocalModelManager.set_device
---

# Choose a device for local transcription

## Trigger

The engine has started and reported its devices, and the user picks one of them or Automatic.

## Outcome

Later local transcription uses the chosen device; Automatic picks the fastest one.
