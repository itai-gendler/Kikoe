---
kind: primary
routes:
  desktop: Desktop
steps:
- text: Reset provider transcription defaults.
  kind: actor
  entities:
  - entity: provider
    effect: reads
    facts: []
  contexts:
    desktop:
      place: desktop::provider
  actor: user
- text: Restore provider parallelism, chunk duration, chunk size and audio format defaults.
  kind: product
  entities:
  - entity: provider
    effect: changes
    facts:
    - Upload settings
  contexts:
    desktop:
      place: desktop::provider
  actor: user
references:
- kind: code
  role: implementation
  target: src/kikoe/ui/provider_page.py#ProviderPage._on_reset_upload_activated
- kind: code
  role: implementation
  target: src/kikoe/core/provider_registry.py
---

# Reset transcription defaults

## Trigger

The user chooses Reset Transcription Defaults on a provider.

## Outcome

Parallel Requests, Chunk Length, Chunk Size and Audio Format return to the API’s defaults for later work.
