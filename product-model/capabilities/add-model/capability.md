---
availability:
- place: desktop
references:
- kind: code
  role: implementation
  target: src/kikoe/ui/model_dialog.py
- kind: code
  role: implementation
  target: src/kikoe/storage/providers.py#ProviderRepository.save_model
- kind: code
  role: implementation
  target: src/kikoe/core/model_catalog.py
domain: providers
---

# Add model

Add a model to a saved provider: its model ID, display name, and separate file and realtime support. Presets for known model IDs fill in the supported options.
