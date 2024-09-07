# Variables And Parameters

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
