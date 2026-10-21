---
entities:
- entity: provider
  shows:
  - Name
  - API type
  - Base URL
  - API key
  - Upload settings
  - Audio LLM settings
  collects:
  - Name
  - API type
  - Base URL
  - API key
  - Upload settings
  - Audio LLM settings
- entity: model
  shows:
  - Model ID
  - Display name
  - File support
  - Realtime support
  collects:
  - Model ID
  - Display name
  - File support
  - Realtime support
references:
- kind: code
  role: implementation
  target: src/kikoe/ui/provider_page.py
- kind: code
  role: implementation
  target: src/kikoe/ui/model_dialog.py
---

# Provider

Create or edit a connection, its upload and prompted-transcription settings, and the model definitions it offers.
