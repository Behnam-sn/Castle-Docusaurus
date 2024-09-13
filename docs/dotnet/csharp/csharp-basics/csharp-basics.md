# C# Basics

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
