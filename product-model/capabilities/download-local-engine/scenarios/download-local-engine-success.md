---
kind: primary
routes:
  desktop: Desktop
steps:
- text: Download the selected local engine build.
  kind: actor
  entities:
  - entity: local-engine
    effect: reads
    facts: []
  contexts:
    desktop:
      place: desktop::local-models
  actor: user
- text: Download the local engine and show progress.
  kind: product
  entities:
  - entity: local-engine
    effect: changes
    facts:
    - Acceleration
    - Download progress
    from: Not downloaded
    to: Downloading
  contexts:
    desktop:
      place: desktop::local-models
  actor: user
- text: Install the local engine and check readiness.
  kind: product
  entities:
  - entity: local-engine
    effect: changes
    facts:
    - Version
    - Acceleration
    - Download progress
    - Readiness
    from: Downloading
    to: Installed
  contexts:
    desktop:
      place: desktop::local-models
  actor: user
references:
- kind: code
  role: implementation
  target: src/kikoe/services/local_models.py#LocalModelManager.install_engine
- kind: code
  role: implementation
  target: src/kikoe/storage/local_installs.py
- kind: code
  role: implementation
  target: src/kikoe/ui/local_engine_group.py
---

# Install a local engine

## Trigger

The user selects an available acceleration build and Download.

## Outcome

The local engine is installed and its readiness and available devices are shown.

## Edge cases

- The recommendation prefers Metal or Vulkan when available, otherwise CPU; CUDA is not the default.
- Each engine has at most one download at a time.
