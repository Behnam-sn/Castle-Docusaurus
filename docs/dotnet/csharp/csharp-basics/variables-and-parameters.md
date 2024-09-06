# Variables And Parameters

A variable represents a storage location that has a modifiable value.

A variable can be a local variable, parameter (value, ref, or out, or in), field (instance or static), or array element.

## The Stack And The Heap

The stack and the heap are the places where variables reside. Each has very different lifetime semantics.

### Stack

The stack is a block of memory for storing local variables and parameters.

The stack logically grows and shrinks as a method or function is entered and exited.

Consider the following method:  
(To avoid distraction, input argument checking is ignored)

```cs
static int Factorial (int x)
{
    if (x == 0)
    {
        return 1;
    }

    return x * Factorial (x-1);
}
```

This method is recursive,  
Meaning that it calls itself.

Each time the method is entered,  
A new int is allocated on the stack,  
And each time the method exits,  
The int is de-allocated.

### Heap

The heap is the memory in which objects (i.e., reference-type instances) reside.

Whenever a new object is created,  
It is allocated on the heap,  
And a reference to that object is returned.

During a program’s execution,  
The heap begins filling up as new objects are created.

The runtime has a garbage collector that periodically de-allocates objects from the heap,  
So your program does not run out of memory.

An object is eligible for de-allocation as soon as it’s not referenced by anything that’s itself _alive_.

In the following example,  
We begin by creating a `StringBuilder` object referenced by the variable `ref1`,  
And then write out its content.

That `StringBuilder` object is then immediately eligible for garbage collection because nothing subsequently uses it.

Then, we create another `StringBuilder` referenced by variable `ref2`,  
And copy that reference to `ref3`.

Even though `ref2` is not used after that point,  
`ref3` keeps the same `StringBuilder` object alive,
Ensuring that it doesn’t become eligible for collection until we’ve finished using `ref3`:

```cs
using System;
using System.Text;

var ref1 = new StringBuilder("object1");
Console.WriteLine (ref1);
// The StringBuilder referenced by ref1 is now eligible for GC.

var ref2 = new StringBuilder("object2");
var ref3 = ref2;
// The StringBuilder referenced by ref2 is NOT yet eligible for GC.

Console.WriteLine (ref3); // object2
```

Value-type instances (and object references) live wherever the variable was declared.

If the instance was declared as a field within a class type,  
Or as an array element,  
That instance lives on the heap.

You can’t explicitly delete objects in C#, as you can in C++.  
An unreferenced object is eventually collected by the garbage collector.

The heap also stores static fields.  
Unlike objects allocated on the heap (which can be garbage-collected),  
These live until the process ends.

## Definite Assignment

C# enforces a definite assignment policy.

In practice,  
This means that outside of an `unsafe` or `interop` context,  
You can’t accidentally access uninitialized memory.

Definite assignment has three implications:

- Local variables must be assigned a value before they can be read.

- Function arguments must be supplied when a method is called (unless marked as optional).

- All other variables (such as fields and array elements) are automatically initialized by the runtime.

For example,  
The following code results in a compile-time error:

```cs
int x;
Console.WriteLine(x); // Compile-time error
```

Fields and array elements are automatically initialized with the default values for their type.

The following code outputs 0,  
Because array elements are implicitly assigned to their default values:

```cs
var ints = new int[2];
Console.WriteLine(ints[0]); // 0
```

The following code outputs 0,  
Because fields are implicitly assigned a default value (whether instance or static):

```cs
Console.WriteLine(Test.X); // 0

class Test
{
    public static int x;
}
```

<!-- ## Default Values

All type instances have a default value.

The default value for the predefined types is the result of a bitwise zeroing of memory:

| Type Default                               | value |
| :----------------------------------------- | :---- |
| Reference types (and nullable value types) | null  |
| Numeric and enum types                     | 0     |
| char type                                  | '\0'  |
| bool type                                  | false |

You can obtain the default value for any type via the default keyword:

```cs
Console.WriteLine(default(decimal)); // 0
```

You can optionally omit the type when it can be inferred:

```cs
decimal d = default;
```

The default value in a custom value type (i.e., struct),
Is the same as the default value for each field defined by the custom type. -->

## Parameters

A method may have a sequence of parameters.  
Parameters define the set of arguments that must be provided for that method.

In the following example,  
The method `Foo` has a single parameter named `p`, of type `int`:

```cs
Foo(8); // 8 is an argument

static void Foo(int p) {...} // p is a parameter
```

You can control how parameters are passed with the `ref`, `in`, and `out` modifiers:

| Parameter modifier | Passed by             | Variable must be definitely assigned |
| :----------------- | :-------------------- | :----------------------------------- |
| (None)             | Value                 | Going in                             |
| ref                | Reference             | Going in                             |
| in                 | Reference (read-only) | Going in                             |
| out                | Reference             | Going out                            |

### Passing Arguments By Value

By default,  
Arguments in C# are passed by value,  
Which is by far the most common case.

This means that a copy of the value is created when passed to the method:

```cs
int x = 8;
Foo(x); // Make a copy of x
Console.WriteLine(x); // x will still be 8

static void Foo(int p)
{
    p = p + 1; // Increment p by 1
    Console.WriteLine(p); // Write p to screen
}
```

Assigning `p` a new value does not change the contents of `x`,  
Because `p` and `x` reside in different memory locations.

Passing a reference-type argument by value copies the reference but not the object.

In the following example,  
`Foo` sees the same `StringBuilder` object we instantiated (`sb`),  
But has an independent reference to it.

In other words, `sb` and `fooSB` are separate variables,  
That reference the same `StringBuilder` object:

```cs
var sb = new StringBuilder();
Foo(sb);
Console.WriteLine(sb.ToString()); // test

static void Fo (StringBuilder fooSB)
{
    fooSB.Append("test");
    fooSB = null;
}
```

Because `fooSB` is a copy of a reference,  
Setting it to `null` doesn’t make `sb` `null`.

(If, however, `fooSB` was declared and called with the `ref` modifier, `sb` would become `null`.)

### The ref Modifier

To pass by reference,  
C# provides the `ref` parameter modifier.

In the following example, `p` and `x` refer to the same memory locations:

```cs
int x = 8;
Foo(ref x); // Ask Foo to deal directly with x
Console.WriteLine(x); // x is now 9

static void Foo(ref int p)
{
    p = p + 1; // Increment p by 1
    Console.WriteLine(p); // Write p to screen
}
```

Now assigning `p` a new value changes the contents of `x`.

Notice how the `ref` modifier is required both when writing and when calling the method.  
This makes it very clear what’s going on.

The ref modifier is essential in implementing a swap method:

```cs
var x = "Penn";
var y = "Teller";

Swap(ref x, ref y);

Console.WriteLine(x); // Teller
Console.WriteLine(y); // Penn

static void Swap(ref string a, ref string b)
{
    var temp = a;
    a = b;
    b = temp;
}
```

### The Out Modifier

An `out` argument is like a `ref` argument except for the following:

- It doesn't need to be assigned before going into the function.
- It must be assigned before it comes out of the function.

The `out` modifier is most commonly used to get multiple return values back from a method;  
For example:

```cs
string a, b;
Split("Stevie Ray Vaughn", out a, out b);
Console.WriteLine(a); // Stevie Ray
Console.WriteLine(b); // Vaughn

void Split(string name, out string firstNames, out string lastName)
{
    var i = name.LastIndexOf(' ');
    firstNames = name.Substring(0, i);
    lastName = name.Substring(i + 1);
}
```

Like a `ref` parameter, an `out` parameter is passed by reference.

### Out Variables And Discards

You can declare variables on the fly when calling methods with `out` parameters.  
We can replace the first two lines in our preceding example with this:

```cs
Split("Stevie Ray Vaughan", out string a, out string b);
```

When calling methods with multiple `out` parameters,  
Sometimes you’re not interested in receiving values from all the parameters.

In such cases,  
You can “discard” the ones in which you’re uninterested by using an underscore:

```cs
Split("Stevie Ray Vaughan", out string a, out _); // Discard 2nd param
Console.WriteLine(a);
```

In this case,  
The compiler treats the underscore as a special symbol, called a discard.

You can include multiple discards in a single call.  
Assuming `SomeBigMethod` has been defined with seven `out` parameters,  
We can ignore all but the fourth,  
As follows:

```cs
SomeBigMethod(out _, out _, out _, out int x, out _, out _, out _);
```

For backward compatibility,  
This language feature will not take effect if a real underscore variable is in scope:

```cs
string _;
Split("Stevie Ray Vaughan", out string a, out _);
Console.WriteLine(_); // Vaughan
```

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
