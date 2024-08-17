# Notes

Unlike .NET Framework, .NET 8 assemblies never have a .exe
extension. The .exe that you see after building a .NET 8
application is a platform-specific native loader responsible for
starting your application’s .dll assembly.
.NET 8 also allows you to create a self-contained deployment
that includes the loader, your assemblies, and the required
portions of the .NET runtime—all in a single .exe file. .NET
8 also allows ahead-of-time (AOT) compilation, where the
executable contains precompiled native code for faster startup
and reduced memory consumption.
