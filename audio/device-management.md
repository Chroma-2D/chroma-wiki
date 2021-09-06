---
title: Device Management
description: Let the sound be heard through a device of your own choosing
published: false
date: 2021-09-06T16:28:16.681Z
tags: 
editor: markdown
dateCreated: 2021-09-06T15:36:34.513Z
---

## Namespaces
[Chroma.Audio](https://chroma-2d.github.io/apiref/namespaceChroma_1_1Audio.html)

## Introduction
The audio sub-system in Chroma allows you to interface with many of the audio devices connected to your computer. When your game boots up, the framework opens the currently designated system output device and provides a _<span title="That is, whatever the developer decided is reasonable...">*reasonable*</span>_ default for the input device. You may want to change that during your game's runtime, and this article is all about it.

### Imports
```CSharp
using Chroma.Audio;
```