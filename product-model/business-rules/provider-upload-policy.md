---
appliesTo:
- type: entity
  id: provider
references:
- kind: code
  role: implementation
  target: src/kikoe/core/provider_registry.py
- kind: code
  role: implementation
  target: src/kikoe/core/upload.py
- kind: code
  role: implementation
  target: src/kikoe/providers/gemini.py#GeminiClient.upload_limits
- kind: code
  role: implementation
  target: src/kikoe/providers/errors.py
---

# Kikoe upload budgets are local request policy

Kikoe enforces the configured size and duration within its API-specific bounds. Parallel Requests defaults to 2 and ranges from 1 to 32. These local budgets do not grant provider account quota or guarantee external acceptance.

## Local request budgets

| API | Encoded audio budget | Duration bound | Default encoding |
| --- | --- | --- | --- |
| OpenAI | 25 MB | Size governed | WAV |
| OpenAI-compatible, OpenRouter, Groq | 25 MB | Size governed | Ogg Opus |
| Deepgram | 2,000 MB | Size governed | Ogg Opus |
| Gemini | 2,000 MB | 60 minutes; 30 with timestamps or speakers | Ogg Opus |
| Mistral | 500 MB | 60 minutes | Ogg Opus |
| MiMo | 7.5 MB before Base64 | Size governed | MP3 |
| Audio LLM | 14 MB before Base64 | 10 minutes | MP3 |

Sizes use decimal MB. MiMo and Audio LLM offer MP3 or WAV; the other cloud adapters offer Ogg Opus, FLAC, WAV and MP3. Local inference uses WAV and the selected local model’s duration bound.

## External service limits

External services decide account access, credits, rate limits, accepted model options and processing outcomes. Kikoe explains their rejection or unavailability; changing local parallelism does not change service entitlements.
