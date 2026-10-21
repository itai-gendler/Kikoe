---
appliesTo:
- type: entity
  id: recording
  facts:
  - Transcript
  - Timestamps
references:
- kind: code
  role: implementation
  target: src/kikoe/core/validation.py#validate_segment_edit
- kind: code
  role: implementation
  target: src/kikoe/storage/library.py#Library.update_segment
---

# Edited passages require text and ordered times

Saved passage text must be nonempty after trimming. Either time may be cleared; when both are supplied the end must be strictly later than the start.
