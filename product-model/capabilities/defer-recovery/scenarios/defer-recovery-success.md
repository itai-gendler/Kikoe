---
kind: primary
routes:
  desktop: Desktop
steps:
- text: Choose Later.
  kind: actor
  entities: []
  contexts:
    desktop:
      place: desktop
  actor: user
- text: Leave the interrupted microphone capture available for another startup.
  kind: product
  entities:
  - entity: microphone-capture
    effect: reads
    facts:
    - Destination
    - Started
    - Audio
    - Elapsed
    - Model and options
    - Confirmed text
    - Connection
  contexts:
    desktop:
      place: desktop
  actor: user
references:
- kind: code
  role: implementation
  target: src/kikoe/ui/recovery_prompt.py
- kind: code
  role: implementation
  target: src/kikoe/ui/recording_controller.py#RecordingController.offer_recovery
---

# Recover later

## Trigger

Startup offers to recover unfinished recordings and the user chooses Later.

## Outcome

Nothing is recovered or uploaded now; the unfinished recordings are offered again at the next startup.
