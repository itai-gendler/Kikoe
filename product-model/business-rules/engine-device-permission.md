---
appliesTo:
- type: entity
  id: local-engine
  effect: changes
  facts:
  - Device
permits:
- actors:
  - user
references:
- kind: code
  role: implementation
  target: src/kikoe/services/local_models.py#LocalModelManager.set_device
---

# Users choose a local engine device

The user may choose Automatic or a device reported by an installed engine, including an engine included with Kikoe.
