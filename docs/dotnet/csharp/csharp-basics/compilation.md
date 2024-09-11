# Compilation

## Assembly

The C# compiler compiles source code (a set of files with the .cs extension) into an assembly.  
An assembly is the unit of packaging and deployment in .NET.

### Assembly Types

An assembly can be either an application or a library.

A normal console or Windows application has an entry point,  
Whereas a library does not.

The purpose of a library is to be called upon (referenced),  
By an application or by other libraries.

.NET itself is a set of libraries (as well as a runtime environment).

## Dotnet Tools

The dotnet tool (dotnet.exe on Windows),  
Helps you to manage .NET source code and binaries from the command line.

You can use it to both build and run your program,  
As an alternative to using an integrated development environment (IDE) such as Visual Studio or Visual Studio Code.

You can obtain the dotnet tool either by installing the .NET 8 SDK or by installing Visual Studio.

Its default location is `%ProgramFiles%\dotnet` on Windows or `/usr/bin/dotnet` on Ubuntu Linux.

To compile an application,  
The dotnet tool requires a project file as well as one or more C# files.

The following command scaffolds a new console project (creates its basic structure):

```console
dotnet new Console -n MyFirstProgram
```

This creates a subfolder called `MyFirstProgram`,  
Containing a project file called `MyFirstProgram.csproj`,  
And a C# file called `Program.cs` that prints “Hello world”.

To build and run your program,  
Run the following command from the `MyFirstProgram` folder:

```console
dotnet run MyFirstProgram
```

Or, if you just want to build without running:

```console
dotnet build MyFirstProgram.csproj
```

The output assembly will be written to a subdirectory under `bin\debug`.

## References

- C# 12 in a Nutshell - Joseph Albahari - OReilly
