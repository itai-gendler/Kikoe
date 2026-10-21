---
appliesTo:
- type: entity
  id: provider
  facts:
  - API key
references:
- kind: code
  role: implementation
  target: src/kikoe/storage/secrets.py#KeyringSecretStore
- kind: code
  role: implementation
  target: src/kikoe/storage/providers.py
---

# API keys are kept only in the system credential store

Each provider’s API key is saved in the operating system’s credential store and nowhere else. When no credential store is available, saving the key fails with an explanation instead of writing it anywhere else. Removing a provider deletes its key.
