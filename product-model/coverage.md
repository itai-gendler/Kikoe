---
scope: Kikoe desktop capture, file and local transcription, recovery, note editing, speakers, exports
  and their configuration.
method: Static tracing of tracked UI, services, domain logic, adapters and persistence at the pinned source
  revision.
covered:
- description: Desktop note workflows, model selection and preference screens.
  paths:
  - src/kikoe/ui/
  - src/kikoe/application.py
- description: Audio workflow, recovery, editing and installation coordination.
  paths:
  - src/kikoe/services/
- description: Note, transcript, speaker, model, upload and local language logic.
  paths:
  - src/kikoe/core/
- description: Transcription request adapters and local inference client behavior.
  paths:
  - src/kikoe/providers/
- description: Library, retained audio, settings, credentials and local installation persistence.
  paths:
  - src/kikoe/storage/
- description: Media capture, conversion, playback and device resolution.
  paths:
  - src/kikoe/media/
- description: System locale selection and shipped translation catalog selection.
  paths:
  - src/kikoe/i18n.py
  - po/
exclusions:
- description: Release packaging and CI machinery are distribution implementation rather than mapped user
    workflows.
  paths:
  - packaging/
  - .github/
- description: Developer tooling, fixtures and test harnesses do not form supported product interfaces.
  paths:
  - scripts/
  - tests/
- description: Images, icons and styling are visual implementation rather than product behavior.
  paths:
  - data/
  - src/kikoe/ui/icons/
  - src/kikoe/ui/style.css
unmapped:
- description: About, shortcut-help and window geometry behavior are peripheral to audio workflows.
  paths:
  - src/kikoe/application.py
  - src/kikoe/ui/shortcuts.py
  - src/kikoe/ui/window_chrome.py
  - src/kikoe/storage/window_state.py
- description: Diagnostic rotation and redaction internals are outside the user-facing log-folder operation.
  paths:
  - src/kikoe/diagnostics.py
- description: Engine worker transport, hardware ranking and individual catalog artifact matrices are
    not separately modeled.
  paths:
  - src/kikoe/providers/local/worker_host.py
  - src/kikoe/providers/local/worker_main.py
  - src/kikoe/providers/local/hardware.py
  - src/kikoe/providers/local/engines/
limitations: []
---

# Coverage
