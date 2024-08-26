# Type System

## Overview

C# is a strongly typed language.

Every variable and constant has a type,  
As does every expression that evaluates to a value.

Every method declaration specifies a name, the type and kind (value, reference, or output) for each input parameter and for the return value.

The .NET class library defines built-in numeric types, and complex types,  
That represent a wide variety of constructs.

These include the file system, network connections, collections and arrays of objects, and dates.

A typical C# program uses types from the class library and user-defined types that model the concepts that are specific to the program's problem domain.

The information stored in a type can include the following items:

- The storage space that a variable of the type requires.
- The maximum and minimum values that it can represent.
- The members (methods, fields, events, and so on) that it contains.
- The base type it inherits from.
- The interfaces it implements.
- The operations that are permitted.

The compiler uses type information to make sure all operations that are performed in your code are type safe.

For example,  
If you declare a variable of type int,  
The compiler allows you to use the variable in addition and subtraction operations.

If you try to perform those same operations on a variable of type bool,  
The compiler generates an error,  
As shown in the following example:

```cs
int a = 5;
int b = a + 2; //OK

bool test = true;

// Error. Operator '+' cannot be applied to operands of type 'int' and 'bool'.
int c = a + test;
```

The compiler embeds the type information into the executable file as metadata.  
The common language runtime (CLR) uses that metadata at run time to further guarantee type safety when it allocates and reclaims memory.

## Specifying Types In Variable Declarations

When you declare a variable or constant in a program,  
You must either specify its type or use the var keyword to let the compiler infer the type.

The following example shows some variable declarations that use both built-in numeric types and complex user-defined types:

```cs
// Declaration only:
float temperature;
string name;
MyClass myClass;

// Declaration with initializers (four examples):
char firstLetter = 'C';
var limit = 3;
int[] source = [0, 1, 2, 3, 4, 5];
var query = from item in source
            where item <= limit
            select item;
```

The types of method parameters and return values are specified in the method declaration.  
The following signature shows a method that requires an int as an input argument and returns a string:

```cs
private string[] names = ["Spencer", "Sally", "Doug"];

public string GetName(int Id)
{
    if (Id < names.Length)
    {
        return names[Id];
    }
    else
    {
        return String.Empty;
    }
}
```

After you declare a variable,  
You can't redeclare it with a new type,  
And you can't assign a value not compatible with its declared type.

For example,  
You can't declare an `int` and then assign it a Boolean value of `true`.

<!-- However, values can be converted to other types,
For example when they're assigned to new variables or passed as method arguments.

A type conversion that doesn't cause data loss is performed automatically by the compiler.
A conversion that might cause data loss requires a cast in the source code. -->

## Built-In Types

C# provides a standard set of built-in types.  
These includes:

- Integers
- Floating point values
- Boolean expressions
- Text characters
- Decimal values
- And other types of data

There are also built-in string and object types.  
These types are available for you to use in any C# program.

## Custom Types

You use the `struct`, `class`, `interface`, `enum`, and `record` constructs to create your own custom types.  
The .NET class library itself is a collection of custom types that you can use in your own applications.

By default,  
The most frequently used types in the class library are available in any C# program.

Others become available only when you explicitly add a project reference to the assembly that defines them.

After the compiler has a reference to the assembly,  
You can declare variables (and constants) of the types declared in that assembly in source code.

One of the first decisions you make when defining a type is deciding which construct to use for your type.

The following list helps make that initial decision.

There's overlap in the choices.

In most scenarios, more than one option is a reasonable choice.

- If the data storage size is small,  
  No more than 64 bytes,  
  Choose a `struct` or `record struct`.

- If the type is immutable,  
  Or you want non-destructive mutation,  
  Choose a `struct` or `record struct`.

- If your type should have value semantics for equality,  
  choose a `record class` or `record struct`.

- If the type is primarily used for storing data,  
  Not behavior,  
  Choose a `record class` or `record struct`.

- If the type is part of an inheritance hierarchy,  
  Choose a `record class` or a `class`.

- If the type uses polymorphism,  
  Choose a `class`.

- If the primary purpose is behavior,  
  Choose a `class`.

## The Common Type System

It's important to understand two fundamental points about the type system in .NET:

- It supports the principle of inheritance.

- Types can derive from other types,  
  Called base types.

- The derived type inherits (with some restrictions) the methods, properties, and other members of the base type.

- The base type can in turn derive from some other type,  
  In which case the derived type inherits the members of both base types in its inheritance hierarchy.

- All types,  
  Including built-in numeric types such as System.Int32 (C# keyword: int),  
  Derive ultimately from a single base type,  
  Which is System.Object (C# keyword: object).

- This unified type hierarchy is known as the Common Type System (CTS).

- Each type in the CTS is defined as either a value type or a reference type.

- These types include all custom types in the .NET class library and also your own user-defined types.

- Types that you define by using the struct keyword are value types;  
  all the built-in numeric types are structs.

- Types that you define by using the class or record keyword are reference types.

- Reference types and value types have different compile-time rules, and different run-time behavior.

Classes and structs are two of the basic constructs of the common type system in .NET.

Essentially,  
Each is a data structure,  
that encapsulates a set of data and behaviors,  
That belong together as a logical unit.

The data and behaviors are the members of the `class`, `struct`, or `record`.

The members include its methods, properties, events, and so on.

A `class`, `struct`, or `record` declaration is like a blueprint,  
That is used to create instances or objects at run time.

<!-- If you define a `class`, `struct`, or `record` named `Person`,
`Person` is the name of the type.

If you declare and initialize a variable p of type Person, p is said to be an object or instance of Person.

Multiple instances of the same Person type can be created,
And each instance can have different values in its properties and fields. -->

A `class` is a reference type.  
When an object of the type is created,  
The variable to which the object is assigned holds only a reference to that memory.

When the object reference is assigned to a new variable,  
The new variable refers to the original object.

Changes made through one variable are reflected in the other variable because they both refer to the same data.

A `struct` is a value type.

When a struct is created,  
The variable to which the `struct` is assigned holds the `struct`'s actual data.

When the `struct` is assigned to a new variable, it's copied.

The new variable and the original variable therefore contain two separate copies of the same data.  
Changes made to one copy don't affect the other copy.

`Record` types can be either reference types (`record class`) or value types (`record struct`).

Record types contain methods that support value-equality.

In general, `classes` are used to model more complex behavior.

`Classes` typically store data that is intended to be modified after a class object is created.

`Structs` are best suited for small data structures.

`Structs` typically store data that isn't intended to be modified after the `struct` is created.

`Record` types are data structures with additional compiler synthesized members.

`Records` typically store data that isn't intended to be modified after the object is created.

## Value types

Value types derive from `System.ValueType`,  
Which derives from `System.Object`.

Types that derive from `System.ValueType` have special behavior in the CLR.

Value type variables directly contain their values.

The memory for a `struct` is allocated inline in whatever context the variable is declared.

There's no separate heap allocation or garbage collection overhead for value-type variables.

You can declare `record struct` types that are value types and include the synthesized members for records.

There are two categories of value types: `struct` and `enum`.

The built-in numeric types are structs,  
And they have fields and methods that you can access:

```cs
// constant field on type byte.
byte b = byte.MaxValue;
```

But you declare and assign values to them as if they're simple non-aggregate types:

```cs
byte num = 0xA;
int i = 5;
char c = 'Z';
```

Value types are sealed.

You can't derive a type from any value type,  
for example `System.Int32`.

You can't define a `struct` to inherit from any user-defined class or `struct` because a `struct` can only inherit from `System.ValueType`.

However, a `struct` can implement one or more interfaces.

You can cast a `struct` type to any interface type that it implements.

This cast causes a boxing operation to wrap the struct inside a reference type object on the managed heap.

Boxing operations occur when you pass a value type to a method that takes a `System.Object` or any interface type as an input parameter.

You use the `struct` keyword to create your own custom value types.

Typically, a `struct` is used as a container for a small set of related variables, as shown in the following example:

```cs
public struct Coords
{
    public int x, y;

    public Coords(int p1, int p2)
    {
        x = p1;
        y = p2;
    }
}
```

## More

- [learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/built-in-types](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/built-in-types)
- [learn.microsoft.com/en-us/dotnet/csharp/fundamentals/object-oriented/inheritance](https://learn.microsoft.com/en-us/dotnet/csharp/fundamentals/object-oriented/inheritance)
- [learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/value-types](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/value-types)
- [learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/struct](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/struct)
