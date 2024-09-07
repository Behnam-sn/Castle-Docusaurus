# Parameters

## What Is A Parameter?

Parameters define the set of arguments,  
That must be provided for a method.

In the following example,  
The method `Foo` has a single parameter named `p` of type `int`:

```cs
Foo(8); // 8 is an argument

static void Foo(int p)
{ ... } // p is a parameter
```

## Types Of Passing Arguments

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
var x = 8;
Foo(x); // Make a copy of x
Console.WriteLine(x); // x will still be 8

static void Foo(int p)
{
    p = p + 1; // Increment p by 1
    Console.WriteLine(p); // Write 9 to screen
}
```

Assigning `p` a new value does not change the contents of `x`,  
Because `p` and `x` reside in different memory locations.

:::tip
Passing a reference-type argument by value,  
Copies the reference but not the object.
:::

In the following example,  
`Foo` sees the same `StringBuilder` object we instantiated (`sb`),  
But has an independent reference to it.

In other words,  
`sb` and `fooSB` are separate variables,  
That reference the same `StringBuilder` object:

```cs
var sb = new StringBuilder();
Foo(sb);
Console.WriteLine(sb.ToString()); // test

static void Fo(StringBuilder fooSB)
{
    fooSB.Append("test");
    fooSB = null;
}
```

Because `fooSB` is a copy of a reference,  
Setting it to `null` doesn’t make `sb`, `null`.

<!-- If `fooSB` was declared and called with the `ref` modifier,  
`sb` would become `null`. -->

### The ref Modifier

To pass by reference,  
C# provides the `ref` parameter modifier.

In the following example,  
`p` and `x` refer to the same memory locations:

```cs
var x = 8;
Foo(ref x); // Ask Foo to deal directly with x
Console.WriteLine(x); // x is now 9

static void Foo(ref int p)
{
    p = p + 1; // Increment p by 1
    Console.WriteLine(p); // Write 9 to screen
}
```

Now assigning `p` a new value changes the contents of `x`.

Notice how the `ref` modifier is required both when writing and when calling the method.  
This makes it very clear what’s going on.

The `ref` modifier is essential in implementing a swap method:

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

### The out Modifier

The `out` modifier is most commonly used to get multiple return values back from a method.

An `out` argument is like a `ref` argument except for the following:

- It doesn't need to be assigned before going into the function.
- It must be assigned before it comes out of the function.

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

Like a `ref` parameter,  
An `out` parameter is passed by reference.

#### Out Variables

You can declare variables on the fly when calling methods with `out` parameters.  
We can replace the first two lines in our preceding example with this:

```cs
Split("Stevie Ray Vaughan", out string a, out string b);
```

#### Discards

When calling methods with multiple `out` parameters,  
Sometimes you’re not interested in receiving values from all the parameters.

In such cases,  
You can “discard” the ones in which you’re uninterested by using an underscore:

```cs
Split("Stevie Ray Vaughan", out string a, out _); // Discard 2nd param
Console.WriteLine(a);
```

In this case,  
The compiler treats the underscore as a special symbol,  
Called a discard.

You can include multiple discards in a single call.  
Assuming `SomeBigMethod` has been defined with seven `out` parameters,  
We can ignore all but the fourth, as follows:

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
