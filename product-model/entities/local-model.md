---
domain: local-models
references:
- kind: code
  role: implementation
  target: src/kikoe/core/local_models.py
- kind: code
  role: implementation
  target: src/kikoe/services/local_models.py
- kind: code
  role: implementation
  target: src/kikoe/ui/local_model_list.py
---

# Local model

A downloadable speech-recognition or speaker-detection model used by an available local engine.

## Information kept

- **Name** — The catalog model name and family.
- **Size** — Expected download size.
- **Languages** — Supported languages and any explicit-language requirement.
- **Features** — File timestamps, realtime text and native speaker detection where supplied.
- **Purpose** — Speech recognition or supplemental speaker detection.
- **Download progress** — Downloaded and total size.
- **Engine availability** — Whether the required engine is installed.

## States

### Not downloaded

The model file is absent.

### Downloading

The model is being downloaded.

### Installed

The model file is present; using it also requires its engine.
