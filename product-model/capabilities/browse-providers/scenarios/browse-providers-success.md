---
kind: primary
routes:
  desktop: Desktop
steps:
- text: Choose a provider to inspect.
  kind: actor
  entities:
  - entity: provider
    effect: reads
    facts:
    - Name
    - API type
  contexts:
    desktop:
      place: desktop::providers
  actor: user
- text: Show provider connection fields and model definitions.
  kind: product
  entities:
  - entity: provider
    effect: reads
    facts:
    - Name
    - API type
    - Base URL
    - API key
    - Upload settings
    - Audio LLM settings
  - entity: model
    effect: reads
    facts:
    - Model ID
    - Display name
    - File support
    - Realtime support
  contexts:
    desktop:
      place: desktop::provider
  actor: user
references:
- kind: code
  role: implementation
  target: src/kikoe/ui/preferences.py#PreferencesDialog._refresh_providers
---

# Open a provider

## Trigger

The user picks a provider in Preferences → Providers.

## Outcome

The provider’s connection, upload settings and models are shown, ready to edit.
