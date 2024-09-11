# Type Basics

## What Is A Type?

A type defines the blueprint for a value.

In this example,  
We use two literals of type `int` with values `12` and `30`.  
We also declare a variable of type `int` whose name is `x`:

```cs
int x = 12 * 30;
Console.WriteLine(x);
```

A variable denotes a storage location that can contain different values over time.  
In contrast, a constant always represents the same value:

```cs
const int y = 360;
```

## Predefined Type Examples

Predefined types are types that are specially supported by the compiler.

The `int` type is a predefined type for representing the set of integers that fit into 32 bits of memory, from −231 to 231−1, and is the default type for numeric literals within this range.

You can perform functions such as arithmetic with instances of the int type,  
As follows:

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
