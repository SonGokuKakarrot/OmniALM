# OmniALM
Loud on AliuCord Dc
# Loud Mic (Aliucord Plugin)

This repository contains an **Aliucord-native Java plugin** called `LoudMic`.

> You asked for the new README without diff-style removed lines, so this is the clean full file content.

## What it does

When enabled, `LoudMic` applies an aggressive communication-audio profile:

- Sets audio mode to `MODE_IN_COMMUNICATION`
- Turns speakerphone off
- Unmutes the microphone
- Pushes `STREAM_VOICE_CALL` volume to the device max

When disabled/unloaded, it restores the previous values it captured on start.

