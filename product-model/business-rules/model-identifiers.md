---
appliesTo:
- type: entity
  id: model
references:
- kind: code
  role: implementation
  target: src/kikoe/core/validation.py#validate_model
- kind: code
  role: implementation
  target: src/kikoe/storage/providers.py#ProviderRepository.save_model
---

# Model identifiers are unique within a provider

A model has a nonempty identifier and at least one supported transcription mode. Two providers may configure the same model identifier independently.
