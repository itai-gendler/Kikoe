---
appliesTo:
- type: entity
  id: local-engine
  effect: changes
  to: Not downloaded
references:
- kind: code
  role: implementation
  target: src/kikoe/services/local_models.py#LocalModelManager.remove_engine
permits:
- actors:
  - user
  when:
  - fact: Included with Kikoe
    is: false
---

# Users remove only engines not included with Kikoe

The Remove Engine operation applies to separately installed engines. Bundled engine installations are kept with Kikoe.
