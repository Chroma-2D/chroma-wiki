---
title: Playback
description: Practical examples on how to play audio using Chroma
published: true
date: 2021-09-04T04:15:47.624Z
tags: sound
editor: markdown
dateCreated: 2021-09-03T13:15:07.149Z
---

## Namespaces

[Chroma.Audio](https://chroma-2d.github.io/apiref/namespaceChroma_1_1Audio.html)
[Chroma.Audio.Sources](https://chroma-2d.github.io/apiref/namespaceChroma_1_1Audio_1_1Sources.html)

## Introduction

Chroma supports loading a sound completely into system memory using an instance of the [Sound](https://chroma-2d.github.io/apiref/classChroma_1_1Audio_1_1Sources_1_1Sound.html) class, or as a streaming resource using an instance of the [Music](https://chroma-2d.github.io/apiref/classChroma_1_1Audio_1_1Sources_1_1Music.html) class. If you're feeling adventurous, you can also procedurally generate a sound with an instance of the [Waveform](https://chroma-2d.github.io/apiref/classChroma_1_1Audio_1_1Sources_1_1Waveform.html) class.

### Supported sound formats

The audio subsystem is based on the excellent [SDL_sound](https://icculus.org/SDL_sound/) library, so it supports everything listed on the aforementioned project's page.

### Imports
```CSharp
using Chroma.Audio.Sources;
```

## Examples
Examples assume the code is inside a class deriving from the [Game](https://chroma-2d.github.io/apiref/classChroma_1_1Game.html) base class.

### Loading a sound from file and playing it

You can load a sound by directly invoking the constructor of the [Sound](https://chroma-2d.github.io/apiref/classChroma_1_1Audio_1_1Sources_1_1Sound.html) class, or by using an [IContentProvider](https://chroma-2d.github.io/apiref/interfaceChroma_1_1ContentManagement_1_1IContentProvider.html) implementation, provided it supports the Sound type.

```CSharp
private Sound _mySound;
private Sound _myOtherSound;
private Sound _myOtherOtherSound;

protected override void LoadContent()
{
	// Either using IContentProvider...
	_mySound = Content.Load<Sound>("path/to/sound.wav");

	// ...or by instantiating it directly using a file path...
	_myOtherSound = new Sound("/home/me/Sounds/hahafunny.mp3");

	// ..or by providing a stream.
	using (var fs = new FileStream("/home/me/Sounds/yay.ogg"))
	{
		_myOtherOtherSound = new Sound(fs);
	}
}
```

### Loading a streaming audio source
Music audio source follows the same basic principle as Sound. As such, only IContentProvider example is present here. The playback, pausing, stopping and seeking are common for all classes deriving from [FileBasedAudioSource](https://chroma-2d.github.io/apiref/classChroma_1_1Audio_1_1Sources_1_1FileBasedAudioSource.html).
  
```CSharp
private Music _myMusic;

protected override void LoadContent()
{
	_myMusic = Content.Load<Music>("path/to/music.mp3");
}
```

### Playing, pausing and stopping a previously loaded sound
```CSharp
protected override void KeyPressed(KeyEventArgs e)
{
	if (e.KeyCode == KeyCode.Q)
	{
		_mySound.Play();
	}
	else if (e.KeyCode == KeyCode.W)
	{
		_mySound.Pause();
	}
	else if (e.KeyCode == KeyCode.E)
	{
		_mySound.Stop();
	}
}
```

### Seeking through a file-based audio source
Unlike most game development APIs, Chroma does not use milliseconds for audio source position and time measuring, but rather seconds and fractions of seconds. This was a deliberate design decision. If you really need the milliseconds for whatever reason, you can write an extension method.
```CSharp
// Will skip 1.5 seconds ahead from the current position.
_mySound.Seek(1.5, SeekOrigin.Current);
```
> If the seek target is outside of bounds, the remaining amount of time exceeding the length (in seconds) of the audio source will be wrapped around.
{.is-warning}
```CSharp
// Let's say _mySound is 30 seconds long and 
// the position of playback is now at 25 seconds.
//
// After executing the following, _mySound.Position 
// will be equal to 5.
//
// Similar logic applies to SeekOrigin.End and 
// SeekOrigin.Begin.
//
_mySound.Seek(10, SeekOrigin.Current);
```
#### But I \*really\* want to use milliseconds
No problem with that. Catch:
```CSharp
using System.IO;
using Chroma.Audio.Sources;

public static class FileBasedAudioSourceExtensions
{
	public static void Seek(this FileBasedAudioSource audioSource, long milliseconds, SeekOrigin seekOrigin)
  	=> audioSource.Seek((double)milliseconds / 1000.0, seekOrigin);
}