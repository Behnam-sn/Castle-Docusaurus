# Value Types

## What Is Value Type?

A variable of a value type,  
Contains an instance of the type.

This differs from a variable of a reference type,  
Which contains a reference to an instance of the type.

By default,  
On assignment,  
Passing an argument to a method,  
And returning a method result,  
Variable values are copied.

In the case of value-type variables,  
The corresponding type instances are copied.

<!-- The following example demonstrates that behavior:

```cs
using System;

public struct MutablePoint
{
    public int X;
    public int Y;

    public MutablePoint(int x, int y) => (X, Y) = (x, y);

    public override string ToString() => $"({X}, {Y})";
}

public class Program
{
    public static void Main()
    {
        var p1 = new MutablePoint(1, 2);
        var p2 = p1;
        p2.Y = 200;
        Console.WriteLine($"{nameof(p1)} after {nameof(p2)} is modified: {p1}");
        Console.WriteLine($"{nameof(p2)}: {p2}");

        MutateAndDisplay(p2);
        Console.WriteLine($"{nameof(p2)} after passing to a method: {p2}");
    }

    private static void MutateAndDisplay(MutablePoint p)
    {
        p.X = 100;
        Console.WriteLine($"Point mutated in a method: {p}");
    }
}
// Expected output:
// p1 after p2 is modified: (1, 2)
// p2: (1, 200)
// Point mutated in a method: (100, 200)
// p2 after passing to a method: (1, 200)
```

As the preceding example shows,
Operations on a value-type variable affect only that instance of the value type, stored in the variable.

If a value type contains a data member of a reference type,
Only the reference to the instance of the reference type is copied when a value-type instance is copied.

Both the copy and original value-type instance have access to the same reference-type instance.

The following example demonstrates that behavior:

```cs
using System;
using System.Collections.Generic;

public struct TaggedInteger
{
    public int Number;
    private List<string> tags;

    public TaggedInteger(int n)
    {
        Number = n;
        tags = new List<string>();
    }

    public void AddTag(string tag) => tags.Add(tag);

    public override string ToString() => $"{Number} [{string.Join(", ", tags)}]";
}

public class Program
{
    public static void Main()
    {
        var n1 = new TaggedInteger(0);
        n1.AddTag("A");
        Console.WriteLine(n1);  // output: 0 [A]

        var n2 = n1;
        n2.Number = 7;
        n2.AddTag("B");

        Console.WriteLine(n1);  // output: 0 [A, B]
        Console.WriteLine(n2);  // output: 7 [A, B]
    }
}
``` -->

## Kinds Of Value Types

A value type can be one of the two following kinds:

- ### Struct

  Which encapsulates data and related functionality.

- ### Enum

  Which is defined by a set of named constants and represents a choice or a combination of choices.

## Value Types Constraints

You cannot assign `null` to a variable of a value type,  
Unless it's a nullable value type.

You can use the `struct` constraint to specify that a type parameter is a non-nullable value type.

Both structure and enumeration types satisfy the `struct` constraint.

You can use `System.Enum` in a base class constraint (that is known as the enum constraint) to specify that a type parameter is an enumeration type.

## Built-In Value Types

C# provides the following built-in value types,  
also known as **simple types**:

- Integral numeric types
- Floating-point numeric types
- `bool` that represents a Boolean value
- `char` that represents a Unicode UTF-16 character

All simple types are `struct` types,  
And differ from other `struct` types in that they permit certain additional operations:

- You can use literals to provide a value of a simple type.  
  For example, `'A'` is a literal of the type `char`,  
  And `2001` is a literal of the type `int`.

- You can declare constants of the simple types with the `const` keyword.  
  It's not possible to have constants of other `struct` types.

- Constant expressions,  
  Whose operands are all constants of the simple types,  
  Are evaluated at compile time.

- A value tuple is a value type,  
  But not a simple type.

## Reference

- [learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/value-types](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/value-types)
