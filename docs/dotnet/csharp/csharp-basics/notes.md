# Notes

## Default Values

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
Is the same as the default value for each field defined by the custom type.

## Target-Typed New Expressions

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

## Top level statewment

Each of the programs in the preceding section began directly with a series of statements (called top-level statements).  
The presence of top-level statements implicitly creates an entry point for a console or Windows application.  
(Without top-level statements, a Main method denotes an application’s entry point)

Fields allow the following modifiers:
Static modifierstatic
Access modifierspublic internal private protected
Inheritance modifiernew
Unsafe code modifier unsafe
Read-only modifierreadonly
Threading modifiervolatile

Nonlocal constants allow the following modifiers:
Access modifiers
public internal private protected
Inheritance modifier new

If a parameter name (or any variable name, for that matter)
conflicts with a field name, you can disambiguate by prefixing
the field with a this reference:

```cs
public Panda (string name) => this.name = name;
```

From C# 9, you can also define module initializers, which
execute once per assembly (when the assembly is first loaded).
To define a module initializer, write a static void method
and then apply the [ModuleInitializer] attribute to that
method:

```cs
[System.Runtime.CompilerServices.ModuleInitializer]
internal static void InitAssembly()
{
...
}
```
