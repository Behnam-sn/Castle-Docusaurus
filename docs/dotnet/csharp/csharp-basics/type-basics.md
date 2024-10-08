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

## Predefined Type

Predefined types are types that are specially supported by the compiler.

The `int` type is a predefined type for representing the set of integers that fit into 32 bits of memory, from −231 to 231−1, and is the default type for numeric literals within this range.

You can perform functions such as arithmetic with instances of the int type,  
As follows:

```cs
int x = 12 * 30;
```

Another predefined C# type is string.  
The string type represents a sequence of characters, such as “.NET”.
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

## Custom Types

Just as we can write our own methods,  
We can write our own types.

In this next example,  
We define a custom type named `UnitConverter`,  
It's a class that serves as a blueprint for unit conversions:

```cs
public class UnitConverter
{
    // Field
    int ratio;

    // Constructor
    public UnitConverter(int unitRatio)
    {
        ratio = unitRatio;
    }

    // Method
    public int Convert(int unit)
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

### Members Of A Type

A type contains data members and function members.

The data member of `UnitConverter` is the field called `ratio`.  
The function members of `UnitConverter` are the `Convert` method and the `UnitConverter`’s constructor.

### Symmetry Of Predefined Types And Custom Types

A beautiful aspect of C# is that predefined types and custom types have few differences.

The predefined `int` type serves as a blueprint for integers.  
It holds data—32 bits—and provides function members that use that data, such as `ToString`.

Similarly, our custom `UnitConverter` type acts as a blueprint for unit conversions.  
It holds data—the ratio—and provides function members to use that data.

### Constructors And Instantiation

Data is created by instantiating a type.

Predefined types can be instantiated simply by using a literal such as `12` or `"Hello world"`.

The `new` operator creates instances of a custom type.  
We created and declared an instance of the `UnitConverter` type with this statement:

```cs
var feetToInchesConverter = new UnitConverter(12);
```

Immediately after the `new` operator instantiates an object,  
The object’s constructor is called to perform initialization.

A constructor is defined like a method,  
Except that the method name and return type are reduced to the name of the enclosing type:

```cs
public UnitConverter(int unitRatio)
{
    ratio = unitRatio;
}
```

### Instance Versus Static Members

The data members and function members that operate on the instance of the type are called instance members.

The `UnitConverter`’s `Convert` method and the `int`’s `ToString` method are examples of instance members.  
By default, members are instance members.

Data members and function members that don’t operate on the instance of the type can be marked as `static`.  
To refer to a static member from outside its type,  
You specify its type name rather than an instance.

An example is the `WriteLine` method of the `Console` class.  
Because this is static,  
We call `Console.WriteLine()` and not `new Console().WriteLine()`.

In the following code,  
The instance field `Name` pertains to an instance of a particular `Panda`,  
Whereas `Population` pertains to the set of all `Panda` instances.

We create two instances of the `Panda`,  
Print their names,  
And then print the total population:

```cs
public class Panda
{
    // Instance field
    public string Name;
    // Static field
    public static int Population;
    // Constructor
    public Panda(string n)
    {
        Name = n; // Assign the instance field
        Population = Population + 1; // Increment the static Population field
    }
}
```

```cs
var p1 = new Panda("Pan Dee");
var p2 = new Panda("Pan Dah");

Console.WriteLine(p1.Name); // Pan Dee
Console.WriteLine(p2.Name); // Pan Dah
Console.WriteLine(Panda.Population); // 2
```

Attempting to evaluate `p1.Population` or `Panda.Name` will generate a compile-time error.

### The Public Keyword

The `public` keyword exposes members to other classes.

In this example,  
If the `Name` field in `Panda` was not marked as `public`,  
It would be `private` and could not be accessed from outside the class.

Marking a member `public` is how a type communicates:  
“Here is what I want other types to see,
Everything else is my own private implementation details.”

In object-oriented terms,  
We say that the public members encapsulate the private members of the class.
