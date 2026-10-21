---
kind: primary
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
references:
- kind: code
  role: implementation
  target: src/kikoe/ui/provider_page.py
- kind: code
  role: implementation
  target: src/kikoe/storage/providers.py
---

# Save a provider connection

## Trigger

The user submits Add on a new connection.

## Outcome

The configured service appears in Providers, initially without model definitions.

## Edge cases

- A built-in endpoint is offered when the URL is blank; custom URLs remain when switching API types.
- Credential storage failures are reported.
