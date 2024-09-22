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
