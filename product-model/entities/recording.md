---
domain: notes
references:
- kind: code
  role: implementation
  target: src/kikoe/core/models.py#Recording
- kind: code
  role: implementation
  target: src/kikoe/storage/library.py
---

# Recording

One retained audio item with its transcript, independently replayed, retried, replaced or deleted within a note.

## Information kept

- **Created** — When this audio item was captured or imported.
- **Source** — Microphone recording or imported audio.
- **Duration** — Audio length, excluding capture pauses.
- **Original audio** — The retained original file; microphone audio is saved as lossless FLAC.
- **Provider and model** — Names captured with the result, retained even after configuration removal.
- **Transcript** — Ordered text passages.
- **Timestamps** — Optional start and end times for each passage.
- **Speaker assignments** — Source labels, their note-wide identities and whether matching has been confirmed.

## States

### Pending

Retained audio awaits a successful transcription.

### Ready

A complete transcription succeeded, including a valid empty result.

### Incomplete

Transcription failed, was interrupted or was cancelled; audio remains available.
