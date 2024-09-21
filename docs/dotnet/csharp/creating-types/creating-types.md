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
You can declare multiple fields of the same type in a commaseparated list.

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
