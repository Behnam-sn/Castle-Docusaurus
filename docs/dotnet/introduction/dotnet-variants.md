---
sidebar_position: 3
---

# .NET Variants

## What are NET Variants?

There are multiple variants of .NET,  
Each supporting a different type of app.

The reason for multiple variants is part historical, part technical.

.NET implementations (historical order):

- ### .NET Framework

  .NET Framework is the original .NET implementation that has existed since 2002.

  .NET Framework is optimized for building Windows desktop applications.  
  It provides access to the broad capabilities of Windows and Windows Server.

  It contains additional Windows-specific APIs,  
  Such as APIs for Windows desktop development with Windows Forms and WPF.  
  Also extensively used for Windows-based cloud computing.

  Today .NET Framework is at version 4.8,  
  And it is actively supported, in maintenance.

- ### Mono

  A cross-platform implementation of .NET Framework.

  The original community and open source .NET.  
  Used for Android, iOS, and Wasm apps.

  Mono is a .NET implementation that is mainly used when a small runtime is required.  
  It is the runtime that powers Xamarin applications on Android, macOS, iOS, tvOS, and watchOS,  
  Also powers games built using the Unity engine.

  It supports all of the currently published .NET Standard versions.

  Historically, Mono implemented the larger API of .NET Framework,  
  And emulated some of the most popular capabilities on Unix.  
  It is sometimes used to run .NET applications that rely on those capabilities on Unix.

  Mono is typically used with a just-in-time compiler,  
  But it also features a full static compiler (ahead-of-time compilation) that is used on platforms like iOS.

- ### .NET (Core)

  .NET, previously referred to as .NET Core,  
  Is currently the primary implementation.

  .NET is built on a single code base that supports multiple platforms and many workloads,  
  Such as Windows desktop apps and cross-platform console apps, cloud services, and websites.

  In 2014, Microsoft introduced .NET Core,  
  As a cross-platform, open-source successor to .NET Framework.

  Rethought to handle server and cloud workloads at scale.  
  While remaining significantly compatible with .NET Framework.

  It also runs on Windows, macOS, and Linux.

  This new implementation of .NET,  
  Kept the name .NET Core through version 3.1.

  The next version after .NET Core 3.1,  
  Dropped the "Core" part of the name and was named .NET 5.

  New .NET versions continue to be released annually,  
  Each a major version number higher.

  They include significant new features and often enable new scenarios.

## References

- [learn.microsoft.com/en-us/dotnet/core/introduction](https://learn.microsoft.com/en-us/dotnet/core/introduction)
- [learn.microsoft.com/en-us/dotnet/fundamentals/implementations](https://learn.microsoft.com/en-us/dotnet/fundamentals/implementations)
