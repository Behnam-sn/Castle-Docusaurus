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

## Syntax

C# syntax is inspired by C and C++ syntax.

In this section, we describe C#’s elements of syntax, using the following program:

```cs
using System;

int x = 12 * 30;
Console.WriteLine (x);
```

### Identifiers

Identifiers are names that programmers choose for their classes, methods, variables,
and so on. Here are the identifiers in our example program, in the order in which
they appear:

```bash
System
x
Console
WriteLine
```

An identifier must be a whole word, essentially made up of Unicode characters
starting with a letter or underscore. C# identifiers are case sensitive. By convention,
parameters, local variables, and private fields should be in camel case (e.g., myVaria
ble), and all other identifiers should be in Pascal case (e.g., MyMethod).

### Keywords

Keywords are names that mean something special to the compiler. There are two
keywords in our example program: using and int.

Most keywords are reserved, which means that you can’t use them as identifiers.
Here is the full list of C# reserved keywords:

- `abstract`
- `as`
- `base`
- `bool`
- `break`
- `byte`
- `case`
- `catch`
- `char`
- `checked`
- `class`
- `const`
- `continue`
- `decimal`
- `default`
- `delegate`
- `do`
- `double`
- `else`
- `enum`
- `event`
- `explicit`
- `extern`
- `false`
- `finally`
- `fixed`
- `float`
- `for`
- `foreach`
- `goto`
- `if`
- `implicit`
- `in`
- `int`
- `interface`
- `internal`
- `is`
- `lock`
- `long`
- `namespace`
- `new`
- `null`
- `object`
- `operator`
- `out`
- `override`
- `params`
- `private`
- `protected`
- `public`
- `readonly`
- `record`
- `ref`
- `return`
- `sbyte`
- `sealed`
- `short`
- `sizeof`
- `stackalloc`
- `static`
- `string`
- `struct`
- `switch`
- `this`
- `throw`
- `true`
- `try`
- `typeof`
- `uint`
- `ulong`
- `unchecked`
- `unsafe`
- `ushort`
- `using`
- `virtual`
- `void`
- `volatile`
- `while`

If you really want to use an identifier that clashes with a reserved keyword, you can
do so by qualifying it with the @ prefix. For instance:

```cs
int using = 123;  // Illegal
int @using = 123; // Legal
```

The @ symbol doesn’t form part of the identifier itself. So, @myVariable is the same
as myVariable.

#### Contextual keywords

Some keywords are contextual, meaning that you also can use them as identifiers without an @ symbol:

- `add`
- `alias`
- `and`
- `ascending`
- `async`
- `await`
- `by`
- `descending`
- `dynamic`
- `equals`
- `file`
- `from`
- `get`
- `global`
- `group`
- `init`
- `into`
- `join`
- `let`
- `managed`
- `nameof`
- `nint`
- `not`
- `notnull`
- `nuint`
- `on`
- `or`
- `orderby`
- `partial`
- `remove`
- `required`
- `select`
- `set`
- `unmanaged`
- `value`
- `var`
- `with`
- `when`
- `where`
- `yield`

With contextual keywords, ambiguity cannot arise within the context in which they
are used.

### Literals, Punctuators, and Operators

Literals are primitive pieces of data lexically embedded into the program. The
literals we used in our example program are 12 and 30.

Punctuators help demarcate the structure of the program. An example is the semi‐
colon, which terminates a statement. Statements can wrap multiple lines:

```cs
Console.WriteLine
(1 + 2 + 3 + 4 + 5 + 6 + 7 + 8 + 9 + 10);
```

An operator transforms and combines expressions. Most operators in C# are deno‐
ted with a symbol, such as the multiplication operator, \*.

These are the operators we used in our example
program:

```cs
=
*
.
()
```

A period denotes a member of something (or a decimal point with numeric literals).
Parentheses are used when declaring or calling a method; empty parentheses are
used when the method accepts no arguments. (Parentheses also have other purposes
that you’ll see later in this chapter.) An equals sign performs assignment. (The
double equals sign, ==, performs equality comparison, as you’ll see later.)

### Comments

C# offers two different styles of source-code documentation: single-line comments
and multiline comments. A single-line comment begins with a double forward slash
and continues until the end of the line; for example:

```cs
int x = 3; // Comment about assigning 3 to x
```

A multiline comment begins with /_ and ends with _/; for example:

```cs
int x = 3; /* This is a comment that
              spans two lines */
```

Comments can embed XML documentation tags.
