---
sidebar_position: 2
---

# .NET Implementations

There are multiple variants of .NET, each supporting a different type of app.  
The reason for multiple variants is part historical, part technical.  
.NET implementations (historical order):

## .NET Framework

.NET Framework is the original .NET implementation that has existed since 2002.

.NET Framework is optimized for building Windows desktop applications.
It provides access to the broad capabilities of Windows and Windows Server.  
It contains additional Windows-specific APIs, such as APIs for Windows desktop development with Windows Forms and WPF.  
Also extensively used for Windows-based cloud computing.

Versions 4.5 and later implement .NET Standard, so code that targets .NET Standard can run on those versions of .NET Framework.  
Today .NET Framework is at version 4.8 and remains fully supported by Microsoft.

## Mono

A cross-platform implementation of .NET Framework.  
The original community and open source .NET. Used for Android, iOS, and Wasm apps.

Mono is a .NET implementation that is mainly used when a small runtime is required.  
It is the runtime that powers Xamarin applications on Android, macOS, iOS, tvOS, and watchOS,  
Also powers games built using the Unity engine.  
Mono is focused primarily on a small footprint.

It supports all of the currently published .NET Standard versions.

Historically, Mono implemented the larger API of .NET Framework and emulated some of the most popular capabilities on Unix.  
It is sometimes used to run .NET applications that rely on those capabilities on Unix.

Mono is typically used with a just-in-time compiler, but it also features a full static compiler (ahead-of-time compilation) that is used on platforms like iOS.

## .NET (Core)

In 2014, Microsoft introduced .NET Core as a cross-platform, open-source successor to .NET Framework.  
Rethought to handle server and cloud workloads at scale.  
while remaining significantly compatible with .NET Framework.  
It also supports other workloads, including desktop apps.  
It runs on Windows, macOS, and Linux.

This new implementation of .NET kept the name .NET Core through version 3.1.  
The next version after .NET Core 3.1 dropped the "Core" part of the name and was named .NET 5.

New .NET versions continue to be released annually, each a major version number higher.  
They include significant new features and often enable new scenarios.

## References

- https://learn.microsoft.com/en-us/dotnet/core/introduction
- https://learn.microsoft.com/en-us/dotnet/fundamentals/implementations
