---
availability:
- place: desktop
references:
- kind: code
  role: implementation
  target: src/kikoe/ui/model_dialog.py#ModelDialog._remove
- kind: code
  role: implementation
  target: src/kikoe/storage/providers.py#ProviderRepository.remove_model
domain: providers
---

# Remove model

Remove a configured model choice from its provider. Stored recordings retain their model attribution.
