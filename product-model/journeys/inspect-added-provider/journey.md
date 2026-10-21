---
actors:
- user
references:
- kind: code
  role: implementation
  target: src/kikoe/ui/provider_page.py#ProviderPage._add
- kind: code
  role: implementation
  target: src/kikoe/ui/preferences.py
---

# Inspect a newly added provider

## Goal

The user adds a provider connection.

## Success criterion

Kikoe returns to Providers and the user opens the saved connection and its model settings.
