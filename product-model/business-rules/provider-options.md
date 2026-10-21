---
appliesTo:
- type: entity
  id: model
references:
- kind: code
  role: implementation
  target: src/kikoe/core/model_catalog.py
- kind: code
  role: implementation
  target: src/kikoe/storage/model_presets.json
- kind: code
  role: implementation
  target: src/kikoe/providers/openai.py
- kind: code
  role: implementation
  target: src/kikoe/providers/groq.py
---

# Requested annotations follow each model mode

File and realtime support are independent. Presets distinguish editable defaults from unsupported options; unsupported options are clamped on saving and loading. OpenAI diarizing file models use their structured response for requested times or speakers. Groq file models omit speaker detection. MiMo and Audio LLM return plain text, while live-only OpenAI, Gemini and Mistral models cannot transcribe files.
