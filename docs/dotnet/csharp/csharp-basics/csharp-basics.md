# C# Basics

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

## Type Basics

A type defines the blueprint for a value. In this example, we use two literals of type
int with values 12 and 30. We also declare a variable of type int whose name is x:

```cs
int x = 12 * 30;
Console.WriteLine (x);
```

A variable denotes a storage location that can contain different values over time.  
In contrast, a constant always represents the same value:

```cs
const int y = 360;
```

### Predefined Type Examples

Predefined types are types that are specially supported by the compiler. The int
type is a predefined type for representing the set of integers that fit into 32 bits of
memory, from −231 to 231−1, and is the default type for numeric literals within this
range. You can perform functions such as arithmetic with instances of the int type,
as follows:

```cs
int x = 12 * 30;
```

Another predefined C# type is string.  
The string type represents a sequence of characters, such as “.NET” or http://oreilly.com.
You can work with strings by calling functions on them, as follows:

```cs
string message = "Hello world";
string upperMessage = message.ToUpper();
Console.WriteLine (upperMessage); // HELLO WORLD
```

```cs
int x = 2022;
message = message + x.ToString();
Console.WriteLine (message); // Hello world2022
```

In this example, we called x.ToString() to obtain a string representation of the
integer x. You can call ToString() on a variable of almost any type.

The predefined bool type has exactly two possible values: true and false.  
The bool type is commonly used with an if statement to conditionally branch execution flow:

```cs
bool simpleVar = false;
if (simpleVar)
Console.WriteLine ("This will not print");
```

```cs
int x = 5000;
bool lessThanAMile = x < 5280;
if (lessThanAMile)
Console.WriteLine ("This will print");
```

:::note
In C#, predefined types (also referred to as built-in types)
are recognized with a C# keyword. The System namespace
in .NET contains many important types that are not prede‐
fined by C# (e.g., DateTime).
:::

### Custom Types

Just as we can write our own methods, we can write our own types. In this next
example, we define a custom type named UnitConverter—a class that serves as a
blueprint for unit conversions:

```cs
public class UnitConverter
{
    int ratio; // Field

    public UnitConverter(int unitRatio) // Constructor
    {
        ratio = unitRatio;
    }

    public int Convert(int unit) // Method
    {
        return unit * ratio;
    }
}
```

```cs
var feetToInchesConverter = new UnitConverter(12);
var milesToFeetConverter = new UnitConverter(5280);

Console.WriteLine(feetToInchesConverter.Convert(30)); // 360
Console.WriteLine(feetToInchesConverter.Convert(100)); // 1200

Console.WriteLine(feetToInchesConverter.Convert(milesToFeetConverter.Convert(1))); // 63360
```

#### Members of a type

A type contains data members and function members. The data member of
UnitConverter is the field called ratio. The function members of UnitConverter
are the Convert method and the UnitConverter’s constructor.

#### Symmetry of predefined types and custom types

A beautiful aspect of C# is that predefined types and custom types have few
differences. The predefined int type serves as a blueprint for integers. It holds
data—32 bits—and provides function members that use that data, such as ToString.
Similarly, our custom UnitConverter type acts as a blueprint for unit conversions. It
holds data—the ratio—and provides function members to use that data.

#### Constructors and instantiation

Data is created by instantiating a type. Predefined types can be instantiated simply
by using a literal such as 12 or "Hello world". The new operator creates instances of
a custom type. We created and declared an instance of the UnitConverter type with
this statement:

```cs
UnitConverter feetToInchesConverter = new UnitConverter (12);
```

Immediately after the new operator instantiates an object, the object’s constructor is
called to perform initialization. A constructor is defined like a method, except that
the method name and return type are reduced to the name of the enclosing type:

```cs
public UnitConverter(int unitRatio)
{
    ratio = unitRatio;
}
```

#### Instance versus static members

The data members and function members that operate on the instance of the type
are called instance members.

The UnitConverter’s Convert method and the int’s
ToString method are examples of instance members. By default, members are
instance members.

Data members and function members that don’t operate on the instance of the type
can be marked as static. To refer to a static member from outside its type, you
specify its type name rather than an instance. An example is the WriteLine method
of the Console class. Because this is static, we call Console.WriteLine() and not
new Console().WriteLine().

(The Console class is actually declared as a static class, which means that all of its
members are static and you can never create instances of a Console.)

In the following code, the instance field Name pertains to an instance of a particular
Panda, whereas Population pertains to the set of all Panda instances. We create two
instances of the Panda, print their names, and then print the total population:

```cs
Panda p1 = new Panda ("Pan Dee");
Panda p2 = new Panda ("Pan Dah");
Console.WriteLine (p1.Name);
Console.WriteLine (p2.Name);
// Pan Dee
// Pan Dah
Console.WriteLine (Panda.Population);
public class Panda
{
public string Name;
public static int Population;
public Panda (string n)
{
Name = n;
Population = Population + 1;
}
// 2
// Instance field
// Static field
// Constructor
// Assign the instance field
// Increment the static Population field
}
```

Attempting to evaluate p1.Population or Panda.Name will generate a compile-time
error.

#### The public keyword

The public keyword exposes members to other classes. In this example, if the Name
field in Panda was not marked as public, it would be private and could not be
accessed from outside the class. Marking a member public is how a type communi‐
cates: “Here is what I want other types to see—everything else is my own private
implementation details.” In object-oriented terms, we say that the public members
encapsulate the private members of the class.

### Top-Level Statements

### Types and Conversions

C# can convert between instances of compatible types. A conversion always creates
a new value from an existing one. Conversions can be either implicit or explicit:
implicit conversions happen automatically, and explicit conversions require a cast.
In the following example, we implicitly convert an int to a long type (which has
twice the bit capacity of an int) and explicitly cast an int to a short type (which
has half the bit capacity of an int):

```cs
int x = 12345;
long y = x;
short z = (short)x;
// int is a 32-bit integer
// Implicit conversion to 64-bit integer
// Explicit conversion to 16-bit integer
```

Implicit conversions are allowed when both of the following are true:

- The compiler can guarantee that they will always succeed.
- No information is lost in conversion.1

Conversely, explicit conversions are required when one of the following is true:

- The compiler cannot guarantee that they will always succeed.
- Information might be lost during conversion.

### Value Types Versus Reference Types

All C# types fall into the following categories:

- Value types
- Reference types
- Generic type parameters
- Pointer types

Value types comprise most built-in types (specifically, all numeric types, the char type, and the bool type) as well as custom struct and enum types.

Reference types comprise all class, array, delegate, and interface types. (This includes the predefined string type.)

The fundamental difference between value types and reference types is how they are handled in memory.

#### Value types

The content of a value type variable or constant is simply a value.  
For example, the content of the built-in value type, int, is 32 bits of data.

You can define a custom value type with the struct keyword:

```cs
public struct Point
{
    public int X;
    public int Y;
}
```

The assignment of a value-type instance always copies the instance; for example:

```cs
Point p1 = new Point();
p1.X = 7;

Point p2 = p1; // Assignment causes copy

Console.WriteLine(p1.X); // 7
Console.WriteLine(p2.X); // 7

p1.X = 9; // Change p1.X

Console.WriteLine(p1.X); // 9
Console.WriteLine(p2.X); // 7

```

#### Reference types

A reference type is more complex than a value type, having two parts: an object and
the reference to that object. The content of a reference-type variable or constant is
a reference to an object that contains the value. Here is the Point type from our
previous example rewritten as a class rather than a struct:

```cs
public class Point
{
    public int X;
    public int Y;
}
```

Assigning a reference-type variable copies the reference, not the object instance.
This allows multiple variables to refer to the same object—something not ordinarily
possible with value types. If we repeat the previous example, but with Point now a
class, an operation to p1 affects p2:

```cs
Point p1 = new Point();
p1.X = 7;

Point p2 = p1; // Copies p1 reference

Console.WriteLine (p1.X); // 7
Console.WriteLine (p2.X); // 7

p1.X = 9; // Change p1.X

Console.WriteLine (p1.X); // 9
Console.WriteLine (p2.X); // 9
```

#### Null

A reference can be assigned the literal null, indicating that the reference points to no object:

```cs
Point p = null;
Console.WriteLine (p == null); // True

// The following line generates a runtime error
// (a NullReferenceException is thrown):
Console.WriteLine (p.X);

class Point {...}
```

In contrast, a value type cannot ordinarily have a null value:

```cs
Point p = null; // Compile-time error
int x = null; // Compile-time error

struct Point {...}
```

#### Storage overhead

Value-type instances occupy precisely the memory required to store their fields.  
In this example, `Point` takes 8 bytes of memory:

```cs
struct Point
{
    int x; // 4 bytes
    int y; // 4 bytes
}
```

:::note
Technically, the CLR positions fields within the type at an
address that’s a multiple of the fields’ size (up to a maximum
of 8 bytes). Thus, the following actually consumes 16 bytes of
memory (with the 7 bytes following the first field “wasted”):

```cs
struct A { byte b; long l; }
```

You can override this behavior by applying the StructLayout
attribute
:::

Reference types require separate allocations of memory for the reference and object.

The object consumes as many bytes as its fields,  
Plus additional administrative overhead.

The precise overhead is intrinsically private to the implementation of the .NET runtime,  
But at minimum, the overhead is 8 bytes,  
Used to store a key to the object’s type,  
As well as temporary information,  
Such as its lock state for multithreading  
And a flag to indicate whether it has been fixed from movement by the garbage collector.

Each reference to an object requires an extra 4 or 8 bytes,  
Depending on whether the .NET runtime is running on a 32- or 64-bit platform.

