# C# Language Basics

## Compilation

The C# compiler compiles source code (a set of files with the .cs extension) into an assembly.

An assembly is the unit of packaging and deployment in .NET.

An assembly can be either an application or a library.

A normal console or Windows application has an entry point, whereas a library does not.

The purpose of a library is to be called upon (referenced) by an application or by other libraries.

.NET itself is a set of libraries (as well as a runtime environment).

Each of the programs in the preceding section began directly with a series of statements (called top-level statements).

The presence of top-level statements implicitly creates an entry point for a console or Windows application.

(Without top-level statements, a Main method denotes an application’s entry point—see “Custom Types” on page 37.)

The dotnet tool (dotnet.exe on Windows) helps you to manage .NET source code and binaries from the command line.

You can use it to both build and run your program,  
As an alternative to using an integrated development environment (IDE) such as Visual Studio or Visual Studio Code.

You can obtain the dotnet tool either by installing the .NET 8 SDK or by installing Visual Studio.

Its default location is %ProgramFiles%\dotnet on Windows or /usr/bin/dotnet on Ubuntu Linux.

To compile an application, the dotnet tool requires a project file as well as one or
more C# files. The following command scaffolds a new console project (creates its
basic structure):
dotnet new Console -n MyFirstProgram

This creates a subfolder called MyFirstProgram containing a project file called
MyFirstProgram.csproj and a C# file called Program.cs that prints “Hello world.”

To build and run your program, run the following command from the MyFirstPro‐
gram folder:
dotnet run MyFirstProgram
Or, if you just want to build without running:
dotnet build MyFirstProgram.csproj

The output assembly will be written to a subdirectory under bin\debug.
We explain assemblies in detail in Chapter 17
