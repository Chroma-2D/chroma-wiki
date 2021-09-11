---
title: Contribution Guidelines
description: Helping you helps us help you help us all
published: true
date: 2021-09-11T05:05:25.726Z
tags: 
editor: markdown
dateCreated: 2021-09-04T21:19:26.255Z
---

>These guidelines assume you are familiar with Markdown and [Wiki.js](https://js.wiki). You are urged to familiarize yourself with the mentioned systems before you continue.
{.is-warning}

>The guidelines are a work-in-progress and might be changed if a situation requires it. Make sure to check these frequently - no effort will be made to notify you when the modifications to this pages are made.
{.is-warning}

# Contributing to this Wiki
Only trusted people can edit and publish changes to this Wiki. Everyone else has read-only access. Feel free to [contact me on telegram](https://telegram.me/ciastex8086) if you are interested in contributing to this documentation effort.

### Glossary

**Level 2 header**
A header defined by markdown as `##`.

**Level 3 header**
A header defined by markdown as `###`.

**Level 4 and 5 headers**
Headers defined by markdown as `####` and `#####`, respectively. These are the only headers *not visible* in the table of contents for the page, so they should be used sparingly in order to avoid the user accidentally missing the documentation content.

## Editor recommendation
It is recommended to use the Markdown editor when presented with the choice on the page configuration screen. Failure to do so might - and most likely will - result in your page being converted to conform with this recommendation.

## Creating a page
Before creating a page, think about a good, meaningful title for it and - if a category isn't present already - how to categorize it correctly. Find a minimal set of words that accurately describes your feature. For example, if you wish to describe loading and playing sounds and music, the relevant title would be *Playback* located in the *Audio* category; if you wish to describe how to create a custom content provider, the relevant title would be *Custom Content Provider* located in the *Content* category; and so on.

## Basic feature documentation page structure
A basic feature documentation page needs to contain sections in the order described below. This structure can be altered as needed if the feature described requires it.

### Namespaces
This is a place where you would link the relevant API reference namespaces, so the user knows where to look for more information.

### Introduction
Requires level 2 header. A short introductory paragraph explaining what is the purpose of the feature and anything else that might be relevant to the user before they can start working with it.

### Introduction - Imports
Requires level 3 header. This is a section where you would put the `using` directives required to make the feature "visible" to the user's translation unit.

### Examples
Requires level 2 header. This is a section where you would put practical examples of the user's feature. An example section needs to make the assumptions clear to the user *before* they get to the actual source code. This helps avoid situations like `I copied the code but it does not work! Help!`, which is all too familiar with sources copied from anywhere on the Internet. The sources should be packed into code blocks with CSharp code highlighter. For example:

~~~
```CSharp
 // Your example goes here.
```
~~~

## Linking type names to API reference
If you are referring to a type used in Chroma in your page, make sure to include link it to [the API reference.](https://chroma-2d.github.io/apiref)

## Documenting unexpected behavior
In order to document unexpected behavior, you are required to use a blockquote with `{.is-warning}` style clause. For example:
```
>Crabs have dangerous claws and it is foolish to put your fingers near these if the crab in question is alive.
{.is-warning}
```

### Other style clauses
There are a few other style clauses available. These are:
- `{.is-success}`
Use it to describe a recommended practice while using the documented feature.

- `{.is-error}`
Used it to describe a warning which failure to take note of might lead to hard-to-debug issues or straight out framework crashes.

- `{.is-info}`
Use it to describe facts about features that make the user's life easier, but don't qualify as any of the above.

# Contributing to Chroma
Anyone can clone, modify the clone, and then send a pull request to the upstream repository. If your modifications fail to meet the following guidelines, the core development team will point out what is wrong and might ask you to (re-)visit this page, so it's worth to pay attention to this section.

## Indentation
4 spaces. Tabs are forbidden.

## General layout
Chroma is a monolithic system at its heart. This means every core module goes into the [Chroma](https://github.com/Chroma-2D/Chroma/tree/master/Chroma) sub-project. [Chroma.Natives](https://github.com/Chroma-2D/Chroma/tree/master/Chroma.Natives) is a dependency that's bootstrapped when Chroma first loads into memory. [Chroma.STB](https://github.com/Chroma-2D/Chroma/tree/master/Chroma.STB) contains C# ports of the popular `stb` single-header C library collection.

## Code layout
A class, struct, enum or record should have their own file. There is one exception to this rule and it only applies to private enumerations. This is explained in detail in the *Nested enumerations* section.

### The informational top
The top of a class consists of and follows the logical order of the following list:
1. Fields
2. Delegates
3. Properties
4. Events

These should be ordered from the least accessible on top to the most accessible on bottom. See [Window](https://github.com/Chroma-2D/Chroma/blob/master/Chroma/Windowing/Window.cs) class for a good example of this rule.

### The constructional middle
The middle of a class consists solely of constructors. They are ordered from the least accessible on top, to the most accessible on bottom of the section.

### The functional bottom
The bottom of a class consists exclusively of methods, Contrary to the previous sections, methods are ordered from the most accessible on top, to the least accessible on bottom. Instance methods take precendence over static methods.

### Nested classes
Ideally *do not* nest classes. If absolutely necessary, they must be private and go at the absolute bottom of the parent class.

### Nested enumerations
Same as above, but if absolutely need and defined inside a class, they must be private and go above field declarations.

## Naming
### Fields
>Do not define public fields unless absolutely necessary. Fields are considered implementation details. If you need your class to expose data, use properties instead.
{.is-danger}
#### Private & protected fields
Private and protected fields must use `lowerCamelCase` and must have a single underscore `_` prepended to their names.
```CSharp
private string _myString;

protected int _myProtectedInt;
```
#### Internal, internal protected & public fields
Internal, internal protected and public fields must use PascalCase.
```CSharp
internal string MyString;

internal protected string MyInternalProtectedString;

// Bad. Don't do it. I will yell at you. 
//  ~ vddcore
public int MyPublicField;
```

### Properties
All properties must use PascalCase regardless of their accessibility.
```CSharp
private int MyIntProperty { get; protected set; }

internal string MyStringProperty { get; set; }

public bool MyBoolProperty => false;
```

### Delegates
All delegates must use PascalCase regardless of their accessibility and must have `Delegate` postfix appended.
```CSharp
private delegate void DoStuffNoReturnDelegate(string aParam, bParam);

protected delegate int DoStuffIntDelegate(bool someParameter);

public delegate bool CheckStuffDelegate();
```

### Constructors & methods
All constructors and methods must use PascalCase regardless of their accessibility. Single-statement methods should be [expression-bodied](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/statements-expressions-operators/expression-bodied-members).
```CSharp
public void DoStuff()
  => SingleStatement();
  
internal void DoStuffInternal()
{
  // ...
}

internal protected void DoStuffNobodyElseDoes()
{
  // ...
}
  
protected void ProcessThings(IEnumerable<string> things)
{
  // ...
}

private void PrivatelyDoStuff()
{
  // ...
}
```

#### Method parameters
All method parameters must use `lowerCamelCase`.

#### Local method variables
All local method variables must use `lowerCamelCase`. Prefer `var` over explicit type declaration.