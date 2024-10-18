# Inheritance

A type can inherit from another type to extend or customize the original type.

Inheriting from a type lets you reuse the functionality in that type instead of building it from scratch.

A type can inherit from only a single type but can itself be inherited by many types,  
Thus forming a type hierarchy.

In this example,  
We begin by defining a type called Asset:

```cs
public class Asset
{
    public string Name;
}
```

Next,  
We define types called Stock and House,  
Which will inherit from Asset.

Stock and House get everything an Asset has,  
Plus any additional members that they define:

```cs
public class Stock : Asset // inherits from Asset
{
    public long SharesOwned;
}

public class House : Asset // inherits from Asset
{
    public decimal Mortgage;
}
```

Here’s how we can use these types:

```cs
var msft = new Stock
{
    Name = "MSFT",
    SharesOwned = 1000
};
Console.WriteLine(msft.Name); // MSFT
Console.WriteLine(msft.SharesOwned); // 1000

var mansion = new House
{
    Name = "Mansion",
    Mortgage = 250000
};
Console.WriteLine(mansion.Name); // Mansion
Console.WriteLine(mansion.Mortgage); // 250000
```

The derived types, Stock and House,  
Inherit the Name field from the base type, Asset.

:::tip
A derived type is also called a sub type.
A base type is also called a super type.
:::

## Polymorphism

References are polymorphic.  
This means a variable of type x,  
Can refer to an object that subtypes x.

For instance,  
Consider the following method:

```cs
public static void Display(Asset asset)
{
    System.Console.WriteLine(asset.Name);
}
```

This method can display both a Stock and a House,  
Because they are both Assets:

```cs
var msft = new Stock
{
    Name = "MSFT",
};
var mansion = new House
{
    Name = "Mansion",
};

Display(msft);
Display(mansion);
```

Polymorphism works on the basis that sub types (Stock and House),  
Have all the features of their base type (Asset).

The converse, however, is not true.  
If `Display` was modified to accept a House,  
You could not pass in an Asset:

```cs
Display(new Asset()); // Compile-time error

public static void Display(House house)
{
    System.Console.WriteLine(house.Mortgage);
}
```

## Casting and Reference Conversions

An object reference can be:

- Implicitly upcast to a base type reference
- Explicitly downcast to a sub type reference

Upcasting and downcasting between compatible reference types performs reference conversions:  
A new reference is (logically) created,  
That points to the same object.

An upcast always succeeds;  
A downcast succeeds only if the object is suitably typed.

### Upcasting

An upcast operation creates a base class reference from a subclass reference:

```cs
var msft = new Stock();
Asset a = msft; // Upcast
```

After the upcast,  
Variable a still references the same Stock object as variable msft.  
The object being referenced is not itself altered or converted:

```CS
Console.WriteLine(a == msft); // True
```

Although a and msft refer to the identical object,  
a has a more restrictive view on that object:

```CS
Console.WriteLine(a.Name); // OK
Console.WriteLine(a.SharesOwned); // Compile-time error
```

The last line generates a compile-time error,  
Because the variable a is of type Asset,  
Even though it refers to an object of type Stock.

To get to its SharesOwned field,  
You must downcast the Asset to a Stock.

### Downcasting

A downcast operation creates a subclass reference from a base class reference:

```cs
var msft = new Stock();
Asset a = msft; // Upcast
Stock s = (Stock)a; // Downcast

Console.WriteLine(s.SharesOwned); // <No error>
Console.WriteLine(s == a); // True
Console.WriteLine(s == msft); // True
```

As with an upcast,  
Only references are affected,  
Not the underlying object.

A downcast requires an explicit cast because it can potentially fail at runtime:

```cs
var h = new House();
Asset a = h; // Upcast always succeeds
Stock s = (Stock)a; // Downcast fails: a is not a Stock
```

If a downcast fails,  
An `InvalidCastException` is thrown.

### The As Operator

The as operator performs a downcast that evaluates to null (rather than throwing an exception) if the downcast fails:

```cs
var a = new Asset();
Stock s = a as Stock; // s is null; no exception thrown
```

This is useful when you’re going to subsequently test whether the result is null:

```cs
if (s != null) Console.WriteLine(s.SharesOwned);
```

Without such a test, a cast is advantageous,  
Because if it fails, a more helpful exception is thrown.

We can illustrate by comparing the following two lines of code:

```cs
long shares = ((Stock)a).SharesOwned; // Approach #1
long shares = (a as Stock).SharesOwned; // Approach #2
```

If a is not a Stock,  
The first line throws an `InvalidCastException`,  
Which is an accurate description of what went wrong.

The second line throws a `NullReferenceException`,  
Which is ambiguous.  
Was a not a Stock, or was a null?

Another way of looking at it is that with the cast operator,  
You’re saying to the compiler:  
“I’m certain of a value’s type;  
If I’m wrong,  
There’s a bug in my code,  
So throw an exception!”

Whereas with the as operator,  
You’re uncertain of its type and want to branch according to the outcome at runtime.

The as operator cannot perform custom conversions,  
And it cannot do numeric conversions:

```cs
long x = 3 as long; // Compile-time error
```

The as and cast operators will also perform upcasts,  
Although this is not useful because an implicit conversion will do the job.

### The Is Operator

The is operator tests whether a variable matches a pattern.

C# supports several kinds of patterns,  
The most important being a type pattern,  
Where a type name follows the `is` keyword.

In this context,  
The is operator tests whether a reference conversion would succeed.

In other words,  
Whether an object derives from a specified class (or implements an interface).  
It is often used to test before downcasting:

```cs
if (a is Stock) Console.WriteLine((Stock)a).SharesOwned);
```

The is operator also evaluates to true if an unboxing conversion would succeed.  
However, it does not consider custom or numeric conversions.
