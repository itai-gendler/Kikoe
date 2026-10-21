---
type: desktop-app
actors:
- user
references:
- kind: code
  role: implementation
  target: src/kikoe/application.py
- kind: code
  role: implementation
  target: src/kikoe/ui/window.py
---

# Kikoe desktop

The local person records, imports, reviews and exports notes and configures transcription here. The same desktop contract serves installed cloud and local models. Provider services and local engines are outbound dependencies.
