---
availability:
- place: desktop
references:
- kind: code
  role: implementation
  target: src/kikoe/ui/local_engine_group.py
- kind: code
  role: implementation
  target: src/kikoe/services/local_models.py#LocalModelManager.install_engine
- kind: code
  role: implementation
  target: src/kikoe/storage/local_installs.py
domain: local-models
---

# Switch local engine

Replace an installed downloadable engine with another acceleration build for this platform, keeping local model files.
