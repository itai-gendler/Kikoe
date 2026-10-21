---
domain: notes
references:
- kind: code
  role: implementation
  target: src/kikoe/core/speakers.py
- kind: code
  role: implementation
  target: src/kikoe/storage/library.py#Library._replace_bindings
---

# Speaker

A note-wide person named by the user or initially displayed as Speaker N. Source recognition labels can be reassigned without destroying the independent identities.

## Information kept

- **Name** — A supplied name, or an unnamed identity displayed with its number.
- **Number** — A stable note-wide display number.
