---
kind: primary
routes:
  desktop: Desktop
steps:
- text: Apply General preferences.
  kind: actor
  entities:
  - entity: preferences
    effect: reads
    facts: []
  contexts:
    desktop:
      place: desktop::general
  actor: user
- text: Save preferences for transcription and devices.
  kind: product
  entities:
  - entity: preferences
    effect: changes
    facts:
    - Language
    - Custom vocabulary
    - Live transcription delay
    - Microphone
    - Audio output
  contexts:
    desktop:
      place: desktop::general
  actor: user
references:
- kind: code
  role: implementation
  target: src/kikoe/ui/preferences.py
- kind: code
  role: implementation
  target: src/kikoe/core/preferences.py
- kind: code
  role: implementation
  target: src/kikoe/media/devices.py
---

# Change General settings

## Trigger

The user changes a setting in Preferences → General.

## Outcome

The setting is saved and applies to later transcription and audio; running work keeps what it started with.

## Edge cases

- Blank language means automatic detection where the chosen model supports it; invalid language tags are not saved.
- Vocabulary is split on commas and newlines and deduplicated; at most 100 terms of at most 100 characters are saved.
- Live delay is zero for the service default or 80–2400 milliseconds for Mistral.
- An unavailable saved device remains listed and the system default is used; an active capture keeps its starting device.
- Interface language follows the system independently of transcription language.
