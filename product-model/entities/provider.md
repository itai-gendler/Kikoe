---
domain: providers
relations:
- entity: model
  verb: offers
  cardinality: one-to-many
references:
- kind: code
  role: implementation
  target: src/kikoe/storage/providers.py
- kind: code
  role: implementation
  target: src/kikoe/ui/provider_page.py
- kind: code
  role: implementation
  target: src/kikoe/storage/secrets.py#KeyringSecretStore
---

# Provider

A user-configured transcription connection. The built-in On This Device choice is derived from local installations.

## Information kept

- **Name** — The chosen service label.
- **API type** — Deepgram, OpenAI, OpenAI-compatible, OpenRouter, Gemini AI Studio, MiMo, Groq, Mistral or Audio LLM.
- **Base URL** — The selected endpoint or the API default.
- **API key** — The credential saved in the operating system credential store.
- **Upload settings** — Parallel requests, maximum chunk duration and size, and audio format.
- **Audio LLM settings** — Request format and prompt, used when API type is Audio LLM.
