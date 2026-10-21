---
entities:
- entity: local-engine
  shows:
  - Name
  - Version
  - Acceleration
  - Device
  - Download progress
  - Readiness
  - Included with Kikoe
  collects:
  - Acceleration
  - Device
- entity: local-model
  shows:
  - Name
  - Size
  - Languages
  - Features
  - Purpose
  - Download progress
  - Engine availability
references:
- kind: code
  role: implementation
  target: src/kikoe/ui/local_models_page.py
- kind: code
  role: implementation
  target: src/kikoe/ui/local_engine_group.py
- kind: code
  role: implementation
  target: src/kikoe/ui/local_model_list.py
---

# Local Models

Inspect, download or remove local engines and models, choose acceleration and a device, and see readiness and download progress.
