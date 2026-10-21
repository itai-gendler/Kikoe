---
kind: validation
routes:
  desktop: Desktop
steps:
- text: Submit connection details.
  kind: actor
  entities: []
  contexts:
    desktop:
      place: desktop::provider
  actor: user
- text: Connection details are invalid.
  kind: condition
  entities: []
  contexts:
    desktop:
      place: desktop::provider
- text: Keep input for correction.
  kind: product
  entities: []
  contexts:
    desktop:
      place: desktop::provider
  actor: user
references:
- kind: code
  role: implementation
  target: src/kikoe/ui/provider_page.py
- kind: code
  role: implementation
  target: src/kikoe/storage/providers.py
---

# Reject invalid connection details

## Trigger

A name is blank or an endpoint is missing or malformed.

## Outcome

No provider is added and the invalid field is explained.
