---
kind: primary
result: achieved
routes:
  desktop: Desktop
steps:
- text: Enter connection fields.
  kind: actor
  entities: []
  contexts:
    desktop:
      place: desktop::provider
  actor: user
  capability: add-provider
- text: Save the provider with selected API and settings and return to Providers.
  kind: product
  entities:
  - entity: provider
    effect: creates
    facts:
    - Name
    - API type
    - Base URL
    - API key
    - Upload settings
    - Audio LLM settings
  contexts:
    desktop:
      place: desktop::provider
  actor: user
  capability: add-provider
- text: Show the new provider.
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
  contexts:
    desktop:
      place: desktop::providers
  actor: user
  capability: add-provider
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
  capability: browse-providers
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
  capability: browse-providers
references:
- kind: code
  role: implementation
  target: src/kikoe/ui/provider_page.py#ProviderPage._add
- kind: code
  role: implementation
  target: src/kikoe/ui/preferences.py
---

# Inspect a newly added provider

## Trigger

The user adds a provider connection.

## Outcome

Kikoe returns to Providers and the user opens the saved connection and its model settings.
