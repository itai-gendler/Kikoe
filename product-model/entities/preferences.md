---
singleton: true
references:
- kind: code
  role: implementation
  target: src/kikoe/core/preferences.py
- kind: code
  role: implementation
  target: src/kikoe/ui/preferences.py
- kind: code
  role: implementation
  target: src/kikoe/ui/bottom_bar.py
---

# Preferences

The local transcription and audio defaults and the current model selection.

## Information kept

- **Recent model** — The last selected configured or local model, restored at startup if available.
- **Requested features** — Timestamps and speakers requested in the current window; unsupported selections are remembered for supporting models.
- **Language** — An optional transcription language hint; blank means automatic detection where supported.
- **Custom vocabulary** — Distinct terms supplied for Mistral file transcription.
- **Live transcription delay** — Mistral live delay, or the service default.
- **Microphone** — Saved input device name or System Default.
- **Audio output** — Saved playback device name or System Default.
- **Data folder** — The current application library location.
- **Log folder** — The local diagnostics location.
