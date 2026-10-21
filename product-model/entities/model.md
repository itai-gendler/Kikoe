---
domain: providers
references:
- kind: code
  role: implementation
  target: src/kikoe/ui/model_dialog.py
- kind: code
  role: implementation
  target: src/kikoe/core/model_catalog.py
---

# Model

An editable model definition within a configured provider; the same model ID at another provider is a separate choice.

## Information kept

- **Model ID** — The service model identifier, unique within this provider.
- **Display name** — A user-facing name, defaulting to the model ID when blank.
- **File support** — Whether files are supported, with timestamps, speaker detection and streaming preview options.
- **Realtime support** — Whether live capture is supported, with its own timestamps and speaker detection options.
