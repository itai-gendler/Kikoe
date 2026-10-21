---
appliesTo:
- type: entity
  id: local-engine
  effect: changes
  facts:
  - Acceleration
  - Download progress
  - Version
references:
- kind: code
  role: implementation
  target: src/kikoe/services/local_models.py#LocalModelManager.install_engine
permits:
- actors:
  - user
  when:
  - fact: Included with Kikoe
    is: false
---

# Users replace only engines not included with Kikoe

A downloadable engine may be installed or switched. An engine included with the application is maintained with that installation.
