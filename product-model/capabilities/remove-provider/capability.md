---
availability:
- place: desktop
references:
- kind: code
  role: implementation
  target: src/kikoe/ui/provider_page.py#ProviderPage._on_remove_row_activated
- kind: code
  role: implementation
  target: src/kikoe/storage/providers.py#ProviderRepository.remove_provider
domain: providers
---

# Remove provider

Remove a configured service, its models and credential after confirmation; previously saved notes keep their audio, text and model labels.
