---
id: kikoe
summary: Record or import audio, transcribe with cloud services or local models, and refine and export
  useful notes.
category: productivity
tags:
- audio
- transcription
- notes
authors:
- name: first-storm
license: GPL-3.0-or-later
languages:
- en
- zh-Hans
- zh-Hant
- es
- fr
- de
- ja
- ko
- pt-BR
- ru
- it
- ar
- hi
- id
- tr
limitations:
- Notes and retained audio live in the local application library; there is no account-based synchronization.
- Cloud transcription uses a configured external service; account access, credits and service quotas belong
  to that service.
- Offline transcription requires an available local engine and downloaded model.
- Imports, retries and re-transcription require a model with file transcription support.
- The data folder can be opened from Preferences but cannot be relocated there.
references:
- kind: doc
  role: intent
  target: README.md
- kind: doc
  role: intent
  target: docs/design.md
- kind: code
  role: implementation
  target: src/kikoe/application.py
- kind: code
  role: implementation
  target: src/kikoe/storage/library.py
- kind: code
  role: implementation
  target: src/kikoe/services/local_models.py
- kind: code
  role: implementation
  target: src/kikoe/i18n.py
---

# Kikoe

Kikoe is a desktop application that records microphone audio or imports audio files and turns them into searchable, editable notes. People choose cloud speech-to-text services or installed local models, review transcripts and speakers, and export text, subtitles or retained audio.

## Intent

**Your conversations, turned into useful notes.** Record a meeting, import an interview, or capture a voice memo. Kikoe turns audio into searchable, editable notes with cloud speech-to-text services or models that run on your own computer.
