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

# Edit model

Change an existing model’s ID, display name or supported options within its provider. Saved choices are kept within what the provider’s API supports.
