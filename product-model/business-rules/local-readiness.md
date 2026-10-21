---
appliesTo:
- type: entity
  id: local-engine
- type: entity
  id: local-model
references:
- kind: code
  role: implementation
  target: src/kikoe/services/local_models.py#LocalModelManager.providers
- kind: code
  role: implementation
  target: src/kikoe/core/local_models.py#model_spec
- kind: code
  role: implementation
  target: src/kikoe/providers/local/client.py
---

# Local recognition requires both an engine and a speech model

Only installed speech models with installed engines appear as On This Device choices. A separate speaker-detection model adds speakers to models with timestamps; native speaker detection does not require it. Local recognition does not upload audio.
