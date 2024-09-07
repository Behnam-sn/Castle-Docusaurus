# Variables And Parameters

### Implications Of Passing By Reference

When you pass an argument by reference,  
You alias the storage location of an existing variable rather than create a new storage location.  
In the following example,  
The variables `x` and `y` represent the same instance:

```cs
class Test
{
    static int x;

    static void Main()
    {
        Foo(out x);
    }

    static void Foo(out int y)
    {
        Console.WriteLine(x); // x is 0
        y = 1; // Mutate y
        Console.WriteLine(x); // x is 1
    }
}
```

### The in modifier

An `in` parameter is similar to a `ref` parameter,  
Except that the argument’s value cannot be modified by the method.  
(Doing so generates a compile-time error)

This modifier is most useful when passing a large value type to the method,  
Because it allows the compiler to avoid the overhead of copying the argument prior to passing it in,  
While still protecting the original value from modification.

Overloading solely on the presence of `in` is permitted:

```cs
void Foo(SomeBigStruct a)
{ ... }

void Foo(in SomeBigStruct a)
{ ... }
```

To call the second overload,  
The caller must use the `in` modifier:

```cs
SomeBigStruct x = ...;
Foo(x); // Calls the first overload
Foo(in x); // Calls the second overload
```

When there’s no ambiguity:

```cs
void Bar(in SomeBigStruct a)
{ ... }
```

use of the `in` modifier is optional for the caller:

```cs
Bar(x); // OK (calls the 'in' overload)
Bar(in x); // OK (calls the 'in' overload)
```

### The params Modifier

The `params` modifier,  
If applied to the last parameter of a method,  
Allows the method to accept any number of arguments of a particular type.

The parameter type must be declared as a (single-dimensional) array,  
As shown in the following example:

```cs
int total = Sum(1, 2, 3, 4);
Console.WriteLine(total); // 10

// The call to Sum above is equivalent to:
int total2 = Sum(new int[] { 1, 2, 3, 4 });

int Sum(params int[] ints)
{
    var sum = 0;
    for (var i = 0; i < ints.Length; i++)
    {
        sum += ints [i]; // Increase sum by ints[i]
    }
    return sum;
}
```

:::note
If there are zero arguments in the params position, a zero-length array is created.
:::

### Optional Parameters

Methods, constructors, and indexers can declare optional parameters.

A parameter is optional if it specifies a default value in its declaration:

```cs
void Foo(int x = 23)
{
    Console.WriteLine (x);
}
```

You can omit optional parameters when calling the method:

```cs
Foo(); // 23
```

The default argument of `23` is actually passed to the optional parameter `x`.  
The compiler bakes the value `23` into the compiled code at the calling side.

The preceding call to `Foo` is semantically identical to:

```cs
Foo (23);
```

because the compiler simply substitutes the default value of an optional parameter wherever it is used.

The default value of an optional parameter must be specified by a constant expression,  
A parameterless constructor of a value type,  
Or a default expression.

Optional parameters cannot be marked with `ref` or `out`.

Mandatory parameters must occur before optional parameters,  
In both the method declaration and the method call.

The exception is with `params` arguments,  
Which still always come last.

In the following example,  
The explicit value of `1` is passed to `x`,  
And the default value of `0` is passed to `y`:

```cs
Foo(1); // 1, 0

void Foo(int x = 0, int y = 0)
{
    Console.WriteLine(x + ", " + y);
}
```

You can do the converse,  
Pass a default value to `x` and an explicit value to `y`,  
By combining optional parameters with _named arguments_.

### Named Arguments

Rather than identifying an argument by position,  
You can identify an argument by name:

```cs
Foo(x: 1, y: 2); // 1, 2

void Foo(int x, int y)
{
    Console.WriteLine(x + ", " + y);
}
```

Named arguments can occur in any order.  
The following calls to Foo are semantically identical:

```cs
Foo(x: 1, y: 2);
Foo(y: 2, x: 1);
```

You can mix named and positional arguments:

```cs
Foo (1, y: 2);
```

However, there is a restriction:  
Positional arguments must come before named arguments,  
Unless they are used in the correct position.

So, you could call `Foo` like this:

```cs
Foo(x: 1, 2); // OK. Arguments in the declared positions
```

But not like this:

```cs
Foo(y: 2, 1); // Compile-time error. y isn't in the first position
```

Named arguments are particularly useful in conjunction with optional parameters.  
For instance, consider the following method:

```cs
void Bar(int a = 0, int b = 0, int c = 0, int d = 0)
{ ... }
```

You can call this supplying only a value for `d`, as follows:

```cs
Bar(d: 3);
```

## Ref Locals

A somewhat esoteric feature of C# is that you can define a local variable that references an element in an array or field in an object (from C# 7):

```cs
int[] numbers = { 0, 1, 2, 3, 4 };
ref var numRef = ref numbers[2];
```

In this example, `numRef` is a reference to `numbers[2]`.  
When we modify `numRef`, we modify the array element:

```cs
numRef *= 10;
Console.WriteLine(numRef); // 20
Console.WriteLine(numbers[2]); // 20
```

The target for a ref local must be an array element, field, or local variable;  
It cannot be a property.

_Ref locals_ are intended for specialized micro-optimization scenarios,  
And are typically used in conjunction with _ref returns_.

### Ref Returns

You can return a _ref local_ from a method.  
This is called a _ref return_:

```cs
class Program
{
    static string x = "Old Value";

    static ref string GetX() => ref x; // This method returns a ref

    static void Main()
    {
        ref string xRef = ref GetX(); // Assign result to a ref local
        xRef = "New Value";
        Console.WriteLine(x); // New Value
    }
}
```

If you omit the `ref` modifier on the calling side,  
It reverts to returning an ordinary value:

```cs
string localX = GetX(); // Legal: localX is an ordinary non-ref variable.
```

You also can use `ref` returns when defining a property or indexer:

```cs
static ref string Prop => ref x;
```

Such a property is implicitly writable,  
Despite there being no set accessor:

```cs
Prop = "New Value";
```

You can prevent such modification by using `ref readonly`:

```cs
static ref readonly string Prop => ref x;
```

The `ref readonly` modifier prevents modification,  
While still enabling the performance gain of returning by reference.

The gain would be very small in this case,  
Because `x` is of type `string` (a reference type):  
No matter how long the string,  
The only inefficiency that you can hope to avoid is the copying of a single 32-bit or 64-bit reference.

Real gains can occur with custom value types,  
But only if the `struct` is marked as readonly;  
Otherwise, the compiler will perform a defensive copy.

Attempting to define an explicit set accessor on a `ref` return property or indexer is illegal.

## var Keyword

var or implicitly typed local variables

It is often the case that you declare and initialize a variable in one step.  
If the compiler is able to infer the type from the initialization expression,  
You can use the keyword var in place of the type declaration;  
For example:

```cs
var x = "hello";
var y = new System.Text.StringBuilder();
var z = (float)Math.PI;
```

This is precisely equivalent to the following:

```cs
string x = "hello";
System.Text.StringBuilder y = new System.Text.StringBuilder();
float z = (float)Math.PI;
```

Because of this direct equivalence,  
Implicitly typed variables are statically typed.

For example, the following generates a compile-time error:

```cs
var x = 5;
x = "hello"; // Compile-time error; x is of type int
```

### Target-Typed new Expressions

Another way to reduce lexical repetition is with target-typed `new` expressions (from C# 9):

```cs
System.Text.StringBuilder sb1 = new();
System.Text.StringBuilder sb2 = new("Test");
```

This is precisely equivalent to:

```cs
System.Text.StringBuilder sb1 = new System.Text.StringBuilder();
System.Text.StringBuilder sb2 = new System.Text.StringBuilder ("Test");
```

The principle is that you can call `new`,  
Without specifying a type name,  
If the compiler is able to unambiguously infer it.

Target-typed new expressions are particularly useful when the variable declaration and initialization are in different parts of your code.

A common example is when you want to initialize a field in a constructor:

```cs
class Foo
{
    System.Text.StringBuilder sb;

    public Foo(string initialValue)
    {
        sb = new(initialValue);
    }
}
```

Target-typed `new` expressions are also helpful in the following scenario:

```cs
MyMethod(new ("test"));

void MyMethod(System.Text.StringBuilder sb)
{ ... }
```

## References

- C# 12 in a Nutshell - Joseph Albahari - OReilly
