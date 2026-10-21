---
appliesTo:
- type: capability
  id: import-audio
- type: capability
  id: retry-transcription
- type: capability
  id: retranscribe-recording
- type: capability
  id: change-general-settings
references:
- kind: code
  role: implementation
  target: src/kikoe/providers/mistral.py#_language
- kind: code
  role: implementation
  target: src/kikoe/providers/groq.py
- kind: code
  role: implementation
  target: src/kikoe/providers/mimo.py#asr_language
- kind: code
  role: implementation
  target: src/kikoe/core/llm_prompt.py#render_prompt
- kind: code
  role: implementation
  target: src/kikoe/providers/local/client.py#_language
---

# Language hints follow the selected recognizer

Blank language requests detection where supported. Mistral file requests omit the language when timestamps or speakers are requested; otherwise Mistral and Groq use the primary language code. MiMo forwards Chinese or English hints and otherwise requests automatic detection. Audio LLM adds the hint to its transcription prompt. Local models marked as requiring a language reject missing or unsupported choices.
