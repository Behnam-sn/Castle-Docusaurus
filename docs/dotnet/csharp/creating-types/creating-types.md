# Creating Types

## Classes

A class is the most common kind of reference type.

The simplest possible class declaration is as follows:

```cs
class YourClassName
{
}
```

A more complex class optionally has the following:

### Fields

A field is a variable that is a member of a class or struct; for example:

```cs
class Octopus
{
    string name;
    public int Age = 10;
}
```

There are two popular naming conventions for private fields:  
camel-cased: `firstName`,  
And camel-cased with an underscore: `_firstName`.

The latter convention lets you instantly distinguish private fields from parameters and local variables.

#### The readonly modifier

The `readonly` modifier prevents a field from being modified after construction.  
A read-only field can be assigned only in its declaration,  
Or within the enclosing type’s constructor.

#### Field initialization

Field initialization is optional.  
An uninitialized field has a default value (0, '\0', null, false).

Field initializers run before constructors:

```cs
public int Age = 10;
```

A field initializer can contain expressions and call methods:

```cs
static readonly string TempFolder = System.IO.Path.GetTempPath();
```

#### Declaring multiple fields together

For convenience,  
You can declare multiple fields of the same type in a comma separated list.

This is a convenient way for all the fields to share the same attributes and field modifiers:

```cs
static readonly int legs = 8, eyes = 2;
```

#### Constants

A constant is evaluated statically at compile time,  
And the compiler literally substitutes its value whenever used.

A constant can be `bool`, `char`, `string`, any of the built-in numeric types, or an `enum` type.

A constant is declared with the `const` keyword and must be initialized with a value.  
For example:

```cs
public class Test
{
    public const string Message = "Hello World";
}
```

A constant can serve a similar role to a `static readonly` field,  
But it is much more restrictive,  
Both in the types you can use,  
And in field initialization semantics.

A constant also differs from a `static readonly` field in that the evaluation of the constant occurs at compile time;  
Thus:

```cs
public static double Circumference(double radius)
{
    return 2 * System.Math.PI * radius;
}
```

Is compiled to:

```cs
public static double Circumference(double radius)
{
    return 6.2831853071795862 * radius;
}
```

It makes sense for `PI` to be a constant,  
Because its value is predetermined at compile time.

In contrast,  
A `static readonly` field’s value can potentially differ each time the program is run:

```cs
static readonly DateTime StartupTime = DateTime.Now;
```

A static readonly field is also advantageous when exposing to other assemblies a value that might change in a later version.  
For instance, suppose that assembly X exposes a constant as follows:

```cs
public const decimal ProgramVersion = 2.3;
```

If assembly Y references X and uses this constant,  
The value `2.3` will be baked into assembly Y when compiled.

This means that if X is later recompiled with the constant set to `2.4`,  
Y will still use the old value of 2.3 until Y is recompiled.

A static readonly field avoids this problem.

Another way of looking at this is that any value that might change in the future is not constant by definition;  
Thus, it should not be represented as one.

Constants can also be declared local to a method:

```cs
void Test()
{
    const double twoPI = 2 * System.Math.PI;
    ...
}
```

### Methods

A method performs an action in a series of statements.

A method can receive input data from the caller,  
By specifying parameters,  
And output data back to the caller,  
By specifying a return type.

A method can specify a void return type,  
Indicating that it doesn’t return any value to its caller.

<!-- A method can also output data back to the caller via ref/out parameters. -->

A method’s signature must be unique within the type.  
A method’s signature comprises its name and parameter types in order,  
But not the parameter names, nor the return type.

<!-- Methods allow the following modifiers:
Static modifierstatic
Access modifierspublic internal private protected
Inheritance modifiersnew virtual abstract override sealed
Partial method modifierpartial
Unmanaged code modifiersunsafe extern
Asynchronous code modifier async -->

#### Expression-bodied methods

A method that comprises a single expression,  
Such as:

```cs
int Foo(int x)
{
    return x * 2;
}
```

can be written more tersely as an expression-bodied method.  
A fat arrow replaces the braces and `return` keyword:

```cs
int Foo(int x) => x * 2;
```

Expression-bodied functions can also have a `void` return type:

```cs
void Foo(int x) => Console.WriteLine (x);
```

#### Local methods

You can define a method within another method:

```cs
void WriteCubes()
{
    Console.WriteLine(Cube(3));
    Console.WriteLine(Cube(4));
    Console.WriteLine(Cube(5));

    int Cube(int value) => value * value * value;
}
```

The local method is visible only to the enclosing method.  
This simplifies the containing type,  
And instantly signals to anyone looking at the code that method is used nowhere else.

Another benefit of local methods is that they can access the local variables and parameters of the enclosing method.

Local methods can appear within other function kinds,  
Such as property accessors, constructors, and so on.

You can even put local methods inside other local methods,  
And inside lambda expressions that use a statement block.

Local methods can be iterators or asynchronous.

#### Static local methods

Adding the `static` modifier to a local method (from C# 8),  
Prevents it from seeing the local variables and parameters of the enclosing method.

This helps to reduce coupling and prevents the local method from accidentally referring to variables in the containing method.

#### Local methods and top-level statements

Any methods that you declare in top-level statements are treated as local methods.

This means that (unless marked as static),  
They can access the variables in the top-level statements:

```cs
int x = 3;
Foo();

void Foo() => Console.WriteLine(x);
```

Local methods cannot be overloaded.

This means that methods declared in top-level statements,  
Which are treated as local methods, cannot be overloaded.

#### Overloading methods

Overloading methods means define multiple methods with the same name.

A type can overload methods as long as the signatures are different.  
For example,  
The following methods can all coexist in the same type:

```cs
void Foo(int x) {...}
void Foo(double x) {...}
void Foo(int x, float y) {...}
void Foo(float x, int y) {...}
```

However, the following pairs of methods cannot coexist in the same type,  
Because the return type and the params modifier are not part of a method’s signature:

```cs
void Foo(int x) {...}
float Foo(int x) {...} // Compile-time error

void Goo(int[] x) {...}
void Goo(params int[] x) {...} // Compile-time error
```

Whether a parameter is pass-by-value or pass-by-reference is also part of the signature.  
For example, `Foo(int)` can coexist with either `Foo(ref int)` or `Foo(out int)`.

However, `Foo(ref int)` and `Foo(out int)` cannot coexist:

```cs
void Foo(int x) {...}
void Foo(ref int x) {...} // OK so far
void Foo(out int x) {...} // Compile-time error
```

### Instance Constructors

Constructors run initialization code on a class or struct.

A constructor is defined like a method,  
Except that the method name and return type are reduced to the name of the enclosing type:

```cs
var p = new Panda("Petey"); // Call constructor

public class Panda
{
    string name; // Define field

    public Panda(string n) // Define constructor
    {
        name = n; // Initialization code (set up field)
    }
}
```

Instance constructors allow the following modifiers:

<!--
Access modifiers
public internal private protected
Unmanaged code modifiers unsafe extern -->

Single-statement constructors can also be written as expression-bodied members:

```cs
public Panda(string n) => name = n;
```

#### Overloading constructors

A class or struct may overload constructors.  
To avoid code duplication, one constructor can call another, using the `this` keyword:

```cs
public class Wine
{
    public decimal Price;
    public int Year;

    public Wine(decimal price) => Price = price;
    public Wine(decimal price, int year) : this (price) => Year = year;
}
```

When one constructor calls another,  
The called constructor executes first.

You can pass an expression into another constructor,  
As follows:

```cs
public Wine(decimal price, DateTime year) : this (price, year.Year) { }
```

The expression can access static members of the class but not instance members.

This is enforced because the object has not been initialized by the constructor at this stage,  
So any methods that you call on it are likely to fail.

#### Implicit parameterless constructors

<!-- Todo: Fact Check -->

For classes,  
The C# compiler automatically generates a parameterless public constructor,  
If and only if you do not define any constructors.

However, as soon as you define at least one constructor,  
The parameterless constructor is no longer automatically generated.

#### Constructor and field initialization order

We previously saw that fields can be initialized with default values in their declaration:

```cs
class Player
{
    int shields = 50; // Initialized first
    int health = 100; // Initialized second
}
```

Field initializations occur before the constructor is executed,  
And in the declaration order of the fields.

#### Nonpublic constructors

Some constructors need not be public.

A common reason to have a nonpublic constructor,  
Is to control instance creation via a static method call.

The static method could be used to return an object from a pool rather than creating a new object,  
Or to return various subclasses based on input arguments:

```cs
public class Class1
{
    Class1() {} // Private constructor

    public static Class1 Create(...)
    {
    // Perform custom logic here to return an instance of Class1
    ...
    }
}
```

### Deconstructors

A deconstructor acts as an approximate opposite to a constructor:  
Whereas a constructor typically takes a set of values (as parameters) and assigns them to fields,  
A deconstructor does the reverse and assigns fields back to a set of variables.

A deconstruction method must be called `Deconstruct` and must have one or more out parameters,  
Such as in the following class:

```cs
class Rectangle
{
    public readonly float Width, Height;

    public Rectangle(float width, float height)
    {
        Width = width;
        Height = height;
    }

    public void Deconstruct(out float width, out float height)
    {
        width = Width;
        height = Height;
    }
}
```

The following special syntax calls the deconstructor:

```cs
var rect = new Rectangle(3, 4);
(float width, float height) = rect; // Deconstruction
Console.WriteLine(width + " " + height); // 3 4
```

The second line is the deconstructing call.  
It creates two local variables and then calls the Deconstruct method.

Our deconstructing call is equivalent to the following:

```cs
float width, height;
rect.Deconstruct(out width, out height);
```

Or:

```cs
rect.Deconstruct(out var width, out var height);
```

Deconstructing calls allow implicit typing,  
So we could shorten our call to this:

```cs
(var width, var height) = rect;
```

Or simply this:

```cs
var (width, height) = rect;
```

If the variables into which you’re deconstructing are already defined,  
Omit the types altogether:

```cs
float width, height;
(width, height) = rect;
```

This is called a deconstructing assignment.  
You can use a deconstructing assignment to simplify your class’s constructor:

```cs
public Rectangle(float width, float height) => (Width, Height) = (width, height);
```

You can offer the caller a range of deconstruction options by overloading the Deconstruct method.

:::tip
The Deconstruct method can be an extension method.  
This is a useful trick if you want to deconstruct types that you did not author.
:::

### Object Initializers

To simplify object initialization,  
Any accessible fields or properties of an object can be set via an object initializer directly after construction.  
For example, consider the following class:

```cs
public class Bunny
{
    public string Name;
    public bool LikesCarrots, LikesHumans;

    public Bunny () {}
    public Bunny (string n) => Name = n;
}
```

Using object initializers,  
You can instantiate `Bunny` objects as follows:

```cs
// Note parameterless constructors can omit empty parentheses
var b1 = new Bunny
{
    Name = "Bo",
    LikesCarrots = true,
    LikesHumans = false
};

var b2 = new Bunny("Bo")
{
    LikesCarrots = true,
    LikesHumans = false
};
```

The code to construct `b1` and `b2` is precisely equivalent to the following:

```cs
var temp1 = new Bunny(); // temp1 is a compiler-generated name
temp1.Name = "Bo";
temp1.LikesCarrots = true;
temp1.LikesHumans = false;
var b1 = temp1;

var temp2 = new Bunny("Bo");
temp2.LikesCarrots = true;
temp2.LikesHumans = false;
var b2 = temp2;
```

The temporary variables are to ensure that if an exception is thrown during initialization,  
You can’t end up with a half-initialized object.

#### Object Initializers Versus Optional Parameters

Instead of relying on object initializers,  
We could write `Bunny`’s constructor as follows,  
With one mandatory and two optional parameters:

```cs
public Bunny (string name, bool likesCarrots = false, bool likesHumans = false)
{
    Name = name;
    LikesCarrots = likesCarrots;
    LikesHumans = likesHumans;
}
```

This would allow us to construct a `Bunny` as follows:

```cs
var b1 = new Bunny(name: "Bo", likesCarrots: true);
```

Historically,  
Relying on constructors for object initialization could be advantageous,  
In that it allowed us to make `Bunny`’s fields or properties read-only.

Making fields or properties read-only is good practice,  
When there’s no valid reason for them to change throughout the life of the object.

However in properties, the init modifier that was introduced in C# 9 lets us achieve this goal with object initializers.

Optional parameters have two drawbacks.  
The first is that while their use in constructors allows for read-only types,  
They don’t (easily) allow for non-destructive mutation.

The second drawback of optional parameters is that when used in public libraries,  
They hinder backward compatibility.

This is because the act of adding an optional parameter at a later date,  
Breaks the assembly’s binary compatibility with existing consumers.

This is particularly important when a library is published on NuGet:  
The problem becomes intractable when a consumer references packages A and B,  
If A and B each depend on incompatible versions of L.

The difficulty is that each optional parameter value is baked into the calling site.  
In other words, C# translates our constructor call into this:

```cs
var b1 = new Bunny("Bo", true, false);
```

This is problematic,  
If we instantiate the Bunny class from another assembly,  
And later modify Bunny by adding another optional parameter such as likesCats.

Unless the referencing assembly is also recompiled,  
It will continue to call the (now nonexistent) constructor with three parameters and fail at runtime.

A subtler problem is that if we changed the value of one of the optional parameters,  
Callers in other assemblies would continue to use the old optional value until they were recompiled.

A final consideration is the effect of constructors on subclassing.  
Having multiple constructors with long parameter lists makes subclassing cumbersome;  
Therefore, it can help to keep constructors to a minimum in number and complexity and use object initializers to fill in the details.

### The this Reference

The `this` reference refers to the instance itself.

In the following example,  
The `Marry` method uses `this` to set the `partner`’s mate field:

```cs
public class Panda
{
    public Panda Mate;

    public void Marry(Panda partner)
    {
        Mate = partner;
        partner.Mate = this;
    }
}
```

The `this` reference also disambiguates a local variable or parameter from a field;  
For example:

```cs
public class Test
{
    string name;

    public Test(string name)
    {
        this.name = name;
    }
}
```

The `this` reference is valid only within non-static members of a class or struct.

### Properties

Properties look like fields from the outside,  
But internally they contain logic,  
Like methods do.

For example,  
You can’t tell by looking at the following code whether `CurrentPrice` is a field or a property:

```cs
var msft = new Stock();
msft.CurrentPrice = 30;
msft.CurrentPrice -= 3;
Console.WriteLine(msft.CurrentPrice);
```

A property is declared like a field but with a get/set block added.  
Here’s how to implement `CurrentPrice` as a property:

```cs
public class Stock
{
    decimal currentPrice; // The private "backing" field

    public decimal CurrentPrice // The public property
    {
        get { return currentPrice; }
        set { currentPrice = value; }
    }
}
```

get and set denote property accessors.

The get accessor runs when the property is read.  
It must return a value of the property’s type.

The set accessor runs when the property is assigned.  
It has an implicit parameter named value,  
Of the property’s type that you typically assign to a private field.

Although properties are accessed in the same way as fields,  
They differ in that they give the implementer complete control over getting and setting its value.

This control enables the implementer to choose whatever internal representation is needed without exposing the internal details to the user of the property.  
In this example, the set method could throw an exception if value was outside a valid range of values.

<!-- Properties allow the following modifiers:
Static modifier static
Access modifiers public internal private protected
Inheritance modifiers new virtual abstract override sealed
Un-managed code modifiers unsafe extern -->

#### Read-only and calculated properties

A property is read-only if it specifies only a get accessor,  
And it is write-only if it specifies only a set accessor.  
(Write-only properties are rarely used.)

A property typically has a dedicated backing field to store the underlying data.  
However, a property can also be computed from other data:

```cs
decimal currentPrice, sharesOwned;

public decimal Worth
{
    get { return currentPrice * sharesOwned; }
}
```

#### Expression-bodied properties

You can declare a read-only property,  
Such as the one in the preceding example,
more tersely as an expression-bodied property.  
A fat arrow replaces all the braces and the get and return keywords:

```cs
public decimal Worth => currentPrice * sharesOwned;
```

With a little extra syntax,  
Set accessors can also be expression-bodied:

```cs
public decimal Worth
{
    get => currentPrice * sharesOwned;
    set => sharesOwned = value / currentPrice;
}
```

#### Automatic properties

The most common implementation for a property is a getter and/or setter,  
That simply reads and writes to a private field of the same type as the property.

An automatic property declaration instructs the compiler to provide this implementation.  
We can improve the first example in this section by declaring `CurrentPrice` as an automatic property:

```cs
public class Stock
{
    ...
    public decimal CurrentPrice { get; set; }
}
```

The compiler automatically generates a private backing field of a compiler generated name that cannot be referred to.  
The set accessor can be marked private or protected if you want to expose the property as read-only to other types.

Automatic properties were introduced in C# 3.0.
