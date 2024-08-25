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
