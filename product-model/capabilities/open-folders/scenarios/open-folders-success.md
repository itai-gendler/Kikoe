---
kind: primary
routes:
  desktop: Desktop
steps:
- text: Open the data or log folder.
  kind: actor
  entities: []
  contexts:
    desktop:
      place: desktop::general
  actor: user
- text: Open the requested preferences folder location in the system file manager.
  kind: product
  entities:
  - entity: preferences
    effect: reads
    facts:
    - Data folder
    - Log folder
  contexts:
    desktop:
      place: desktop::general
  actor: user
references:
- kind: code
  role: implementation
  target: src/kikoe/application.py#Application._launch_folder
- kind: code
  role: implementation
  target: src/kikoe/ui/preferences.py
---

# Open folders

## Trigger

The user opens Data Folder or Log Folder in Preferences → General.

## Outcome

The folder opens in the system file manager.

## Edge cases

- Failure to open the folder is explained.
- Opening the data folder does not relocate the library.
