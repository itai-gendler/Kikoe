---
kind: primary
routes:
  desktop: Desktop
steps:
- text: Reset the Audio LLM prompt.
  kind: actor
  entities: []
  contexts:
    desktop:
      place: desktop::provider
  actor: user
- text: Restore the provider prompt to the built-in default.
  kind: product
  entities:
  - entity: provider
    effect: changes
    facts:
    - Audio LLM settings
  contexts:
    desktop:
      place: desktop::provider
  actor: user
references:
- kind: code
  role: implementation
  target: src/kikoe/ui/provider_page.py#ProviderPage._on_reset_prompt_button_clicked
- kind: code
  role: implementation
  target: src/kikoe/core/llm_prompt.py
---

# Reset prompt

## Trigger

The user chooses Reset in the Prompt group of an Audio LLM provider.

## Outcome

The built-in transcription prompt is restored and saved for that provider.
