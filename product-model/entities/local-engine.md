---
domain: local-models
relations:
- entity: local-model
  verb: runs
  cardinality: one-to-many
references:
- kind: code
  role: implementation
  target: src/kikoe/services/local_models.py
- kind: code
  role: implementation
  target: src/kikoe/ui/local_engine_group.py
---

# Local engine

An engine installation used by local speech models, currently transcribe.cpp.

## Information kept

- **Name** — The engine name.
- **Version** — The bundled catalog version of the engine.
- **Acceleration** — The selected platform-compatible build.
- **Device** — Automatic selection or one of the devices the running engine reports.
- **Download progress** — Downloaded and total size during installation.
- **Readiness** — Starting, ready or could not start, with an explanation on failure.
- **Included with Kikoe** — Whether the engine is supplied with the application and managed as part of it.

## States

### Not downloaded

The engine has no installation.

### Downloading

An engine download is in progress.

### Installed

The engine is available locally, including a bundled installation.
