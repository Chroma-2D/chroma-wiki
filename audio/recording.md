---
title: Recording
description: Learn how to capture and use the recorded audio
published: true
date: 2021-09-04T07:12:09.312Z
tags: 
editor: markdown
dateCreated: 2021-09-03T18:36:03.902Z
---

## Namespaces
[Chroma.Audio](https://chroma-2d.github.io/apiref/namespaceChroma_1_1Audio.html)
[Chroma.Audio.Captures](https://chroma-2d.github.io/apiref/namespaceChroma_1_1Audio_1_1Captures.html)

## Introduction
Chroma provides an interface allowing you to easily capture raw audio samples using any capture device supported by the SDL in an audio format that you can decide on. You can extend the [AudioCapture](https://chroma-2d.github.io/apiref/classChroma_1_1Audio_1_1Captures_1_1AudioCapture.html) class yourself, or use the [StreamAudioCapture](https://chroma-2d.github.io/apiref/classChroma_1_1Audio_1_1Captures_1_1StreamAudioCapture.html) class to easily process the captured audio using a stream.

### Imports
```CSharp
using Chroma.Audio.Captures;
```

## Examples
Examples assume the code is inside a class deriving from the [Game](https://chroma-2d.github.io/apiref/classChroma_1_1Game.html) base class. There is [an example project available](https://github.com/Chroma-2D/Chroma/tree/master/Chroma.Examples/AudioRecording) in the Github repository.

### Capturing audio samples to a stream
```CSharp
private StreamAudioCapture _capture;
private FileStream _fileStream;

protected override void KeyPressed(KeyEventArgs e)
{
	if (e.Key == KeyCode.Q)
  {
  	if (_fileStream != null && _capture != null)
    {
    	_capture.Stop();
      _fileStream.Dispose();
    }
    else
    {
			_fileStream = File.OpenOrCreate("/path/to/output.samples");
  		_capture = new StreamAudioCapture(_fileStream);
    
    	_capture.Start();
    }
  }
}
```

### Playing the previously recorded samples back
To do that, you have to be familiar with the way the [Waveform](/audio/waveform) mechanism works. Once you know that, you should be able to understand the following example without any issues. The example below assumes fields set up by the example above.

>This example also makes a very naïve assumption that the file format of the recording matches that of the Waveform created. In a real-world scenario it would be wise to store the file format of the recording and then convert the samples to the actual audio format in the Waveform streaming delegate as you stream the samples to the output device.
{.is-warning}

```CSharp
private Waveform _waveform;

protected override void KeyPressed(KeyEventArgs e)
{
	if (e.Key == KeyCode.W)
  {
		_fileStream = File.Open("/path/to/output.samples", FileMode.OpenOrCreate);
    _waveform = new Waveform(StreamRecordedData);
    _waveform.Play();
  }
}

private void StreamRecordedData(Span<byte> data, AudioFormat format)
{
	var bytesRead = _fileStream.Read(data);
  
  if (bytesRead <= 0)
  {
  	_waveform.Stop();
  }
}
```