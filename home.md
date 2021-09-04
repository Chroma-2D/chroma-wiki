---
title: Main Page
description: Welcome to Chroma Framework!
published: true
date: 2021-09-04T22:34:48.697Z
tags: 
editor: markdown
dateCreated: 2021-09-03T13:00:31.358Z
---

> This documentation is still under construction. Things will be added, changed or completely removed without any warning!
{.is-warning}

<center><img src="/nugeticon.png" /></center>

## Introduction
Ever thought to yourself the following as a C# developer?

> Man, I wish I could just download a single library and start writing the game of my dreams without worrying about all the dependencies and stuff...

The wait is over! Chroma is a fast, intuitive and powerful 2D game development framework with focus on quick prototyping and simplicity without sacrificing functionality. Additionally, you can build and run your game on any supported platform using just a single codebase! 

Chroma is licensed under the very permissive [MIT license](https://github.com/Chroma-2D/Chroma/blob/master/LICENSE.md), which essentially means that you have a choice of extending the framework and sharing your changes with the public, or keeping these completely to yourself. Same goes for your game's code, of course!

Sounds too good to be true, huh?
 
## I don't believe you
`GameCore.cs`
```CSharp
using System.Numerics;
using Chroma;
using Chroma.Graphics;

namespace MyGame
{
	public class GameCore : Game
  {
  	public Game() 
    	: base(new(false, false))
    {
    }
    
    protected override void Draw(RenderContext context)
    	=> context.DrawString("Hello, world!", new Vector2(16, 16));
  }
}
```

`Program.cs`
```CSharp
using System;

namespace MyGame
{
	static class Program
  {
  	static void Main(string[] args)
    	=> new GameCore.Run();
  }
}
```

That's it. This is the minimum required to get something drawn on screen. Convinced yet?

## I still don't believe you
![nugeticon.png](/ayfkm.png)

Fine. Have [the entire list of available examples](https://github.com/Chroma-2D/Chroma/tree/master/Chroma.Examples).

## Why would I use Chroma over MonoGame, Love2DCS or any other framework already out there?
Chroma is designed for the new .NET from the ground up. It does not try to act as a replacement for any pre-existing engines or frameworks and instead tries to take small, good parts of each and make them work together while adding some much needed convenience to aid with quick set-up and cut the boilerplate on the game developer's side of things. It is the answer to the author's frustration with the existing .NET game development libraries:
 - [MonoGame](http://www.monogame.net/)
Too broad for the author's liking. Stays in the box of the "XNA way of doing things". Trivial tasks that should be available out-of-box need external libraries to get done.
 - [Love2DCS](https://github.com/endlesstravel/Love2dCS)
It's taking something designed for Lua into .NET. Essentially playing a catch-up game every time Love2D makes a change or adds a new feature.
 - [Ultraviolet Framework](https://github.com/tlgkccampbell/ultraviolet)
It almost scratched the author's itch, but it was not intuitive enough. There is a trade-off between simplicity and modularity. Ultraviolet takes the latter over the former.

While other libraries certainly have their own strengths and advantages - for example MonoGame and Ultraviolet support mobile platforms, 3D capabilities are a first-class feature, all of them also have their own thriving communities, there is one weakness connecting them all. *They are a hassle to set up and maintain.*

## Supported platforms
Right now Chroma supports Linux, Windows and macOS. 32-bit processors are not supported. Mobile platform support is hesitantly considered, but not being worked on yet. If you need these *right now*, then it may be better for you to look into one of the frameworks listed above.

## Requirements
All Chroma needs is a working .NET 5 (or newer) installation. Once you got that working you can get to the next section.

## Acquiring the library
The library is available for download from the [NuGet package gallery](https://www.nuget.org/packages/Chroma/).

In order to add a package to an existing project, run:
`dotnet add package Chroma --version 0.49.1`

## API reference
API reference is generated automatically and is available at [https://chroma-2d.github.io/apiref](https://chroma-2d.github.io/apiref).

## I found a bug
Wow, paint me surprised! You are most welcome to [publish a Github issue!](https://github.com/Chroma-2D/Chroma/issues)

## I want to help
It would be great to have you on board! Fork Chroma, make your changes and - when you are done - submit a pull request. Then we can talk what can be done about it.  

If you would like to contribute to this documentation effort, [shoot me a message.](https://telegram.me/ciastex8086) I certainly could use some help writing and then maintaining all of this.
  
Not a programmer yourself? Then I can only wonder how did you end down here. However, if you still desperately want to help and got extra money to spare, you can support the project via PayPal.
<center>
<form action="https://www.paypal.com/donate" method="post" target="_top">
<input type="hidden" name="hosted_button_id" value="VXRNGVAKJT36J" />
<input type="image" src="https://www.paypalobjects.com/en_US/i/btn/btn_donate_LG.gif" border="0" name="submit" title="PayPal - The safer, easier way to pay online!" alt="Donate with PayPal button" />
<img alt="" border="0" src="https://www.paypal.com/en_PL/i/scr/pixel.gif" width="1" height="1" />
</form>
</center>