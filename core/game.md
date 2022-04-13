---
title: Game
description: Demystifying the heart of your project
published: true
date: 2022-04-13T18:19:36.435Z
tags: 
editor: markdown
dateCreated: 2021-09-04T23:25:34.140Z
---

## Introduction
The [Game](https://chroma-2d.github.io/index.html#File:Game.cs) base class is the first thing you will see when starting a project utilizing Chroma. It serves as a focal point for all of your state processing, drawing logic, input processing, window operations, and more.

### Imports
```CSharp
using Chroma;
```

### Basic sub-systems
Chroma provides a set of properties allowing you to interact with all of the provided sub-systems.

- **[Window](https://chroma-2d.github.io/index.html#File:Windowing/Window.cs)**
This property allows you to access the window acting as a viewport for your game. You can use it to go fullscreen, ask for user's attention by flashing a window, and many more. You are encouraged to visit [this wiki page](/windowing) for details and examples of using the windowing sub-system.

- **[Graphics](https://chroma-2d.github.io/index.html#File:Graphics/GraphicsManager.cs)**
This property allows you to access and process various details about the graphics adapter, current vertical synchronization mode, available OpenGL extensions and - perhaps most importantly - retrieve available monitors and their supported modes. See more on [this wiki page](/graphics/graphics-manager).

- **[Audio](https://chroma-2d.github.io/apiref/namespaceChroma_1_1Audio.html)**
This property provides access to audio input and output facilities. Please visit [this wiki page](/audio) if you wish to know more about this sub-system.

- **[Content](https://chroma-2d.github.io/apiref/interfaceChroma_1_1ContentManagement_1_1IContentProvider.html)**
This property facilitates easy asset loading. It allows you to load, unload, track and register custom importers for your content. The default implementation available to all games is the [FileSystemContentProvider](https://chroma-2d.github.io/apiref/classChroma_1_1ContentManagement_1_1FileSystem_1_1FileSystemContentProvider.html). Details and articles regarding the content sub-system can be found on [this wiki page](/content). 

### Miscellaneous properties
There are a few other properties you can use to control some of the framework's inner workings, some of them are not as easy to understand as the rest of the framework.

- **[FixedTimeStepTarget](https://chroma-2d.github.io/apiref/classChroma_1_1Game.html#ada713104d136386753bf34e33402c85e)**
This property controls the frequency at which the [FixedUpdate](https://chroma-2d.github.io/apiref/classChroma_1_1Game.html#a9e901c57b9e45dd2711582fb484c517a) callback will be called. Its unit is best described with "call it that many times every second". The default is 75.

- **[StartupOptions](https://chroma-2d.github.io/apiref/classChroma_1_1Game.html#af6210531229f341a150111cb8ab3fcbb)**
This property allows you to access the pre-initialization settings that were passed to the base class constructor. They are read-only and can only be set at the time of instantiation of your game's core class.

### Callbacks
Utilizing the event queue provided by SDL, Chroma provides [a set of callback methods](https://chroma-2d.github.io/apiref/classChroma_1_1Game.html#pro-methods) your game can use to retrieve keyboard, mouse and game controller input, as well as easily check for device (dis-)connection. The callbacks are explained in detail in the Examples section of this document.

## Examples
All of the examples below assume an empty console application project.

### Creating an empty game class with the default scene and bootscreen
The [GameStartupOptions](https://chroma-2d.github.io/apiref/classChroma_1_1GameStartupOptions.html) class enables you to decide whether you want to show the Chroma startup animation, whether Chroma should construct the default scene and how many MSAA samples do you wish to take for anti-aliasing - if supported.

#### `GameCore.cs`
```CSharp
using Chroma;

namespace ExampleGame
{
	public class GameCore : Game
  {
  	public GameCore()
    	: base(new GameStartupOptions(false, false))
    {
    }
  }
}
```

#### `Program.cs`
```CSharp
using Chroma;

namespace ExampleGame
{
	static class Program
  {
  	static void Main(string[] args)
    	=> new GameCore.Run();
  }
}
```