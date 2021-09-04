---
title: Audio
description: Chroma Audio Subsystem
published: true
date: 2021-09-04T21:42:46.941Z
tags: audio
editor: markdown
dateCreated: 2021-09-03T14:29:57.224Z
---

# Audio
Chroma Audio Subsystem is based on SDL_sound to provide audio decoding capabilities and SDL_nmix - a robust and lean audio mixer with bindings to SDL_sound.

## The basics
**[Playback](/audio/playback)**
Load and control static and streaming audio resources.

**[Recording](/audio/recording)**
Record audio using an available audio capture device.

**[Device management](/audio/mixer/devices)**
Configure, open and close available audio devices.

**[Audio parameters](/audio/mixer/parameters)**
Tweak various available audio parameters.

## The not-so-basics
**[Waveform](/audio/playback/waveform)**
Generate arbitrary waveforms using C# ~~and duct tape~~.