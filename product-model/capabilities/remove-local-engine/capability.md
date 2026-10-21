---
availability:
- place: desktop
references:
- kind: code
  role: implementation
  target: src/kikoe/ui/local_engine_group.py#LocalEngineGroup._on_remove_response
- kind: code
  role: implementation
  target: src/kikoe/services/local_models.py#LocalModelManager.remove_engine
domain: local-models
---

# Remove local engine

Remove an installed downloadable engine, keeping its model files unless the user explicitly chooses to remove them too.
