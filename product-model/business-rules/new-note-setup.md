---
appliesTo:
- type: capability
  id: create-note
- type: capability
  id: start-recording
- type: capability
  id: import-audio
references:
- kind: code
  role: implementation
  target: src/kikoe/core/activity.py#action_availability
- kind: code
  role: implementation
  target: src/kikoe/services/local_models.py#LocalModelManager.providers
---

# New Note requires an available provider

The desktop enables explicit New Note only while at least one configured provider or usable built-in local provider exists. Recording and import additionally require an available model. A provider may be configured before it has models.
