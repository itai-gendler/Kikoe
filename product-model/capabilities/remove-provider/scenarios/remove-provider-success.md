---
kind: primary
routes:
  desktop: Desktop
steps:
- text: Confirm provider removal.
  kind: actor
  entities:
  - entity: provider
    effect: reads
    facts: []
  contexts:
    desktop:
      place: desktop::provider
  actor: user
- text: Remove the provider and its model definitions.
  kind: product
  entities:
  - entity: provider
    effect: removes
  - entity: model
    effect: removes
    with: provider
  contexts:
    desktop:
      place: desktop::provider
  actor: user
references:
- kind: code
  role: implementation
  target: src/kikoe/ui/provider_page.py#ProviderPage._on_remove_row_activated
- kind: code
  role: implementation
  target: src/kikoe/storage/providers.py#ProviderRepository.remove_provider
---

# Remove provider

## Trigger

The user chooses Remove Provider and confirms.

## Outcome

The provider, its models and its saved API key are deleted and Kikoe returns to Providers; saved notes keep their audio, text and model names.
