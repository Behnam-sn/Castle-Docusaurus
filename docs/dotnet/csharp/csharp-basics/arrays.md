# Arrays

## What Are Arrays?

An array represents a fixed number of variables (called elements) of a particular type.  
The elements in an array are always stored in a contiguous block of memory,  
Providing highly efficient access.

An array is denoted with square brackets after the element type:

```cs
var vowels = new char[5]; // Declare an array of 5 characters
```

Square brackets also index the array,  
Accessing a particular element by position:

```cs
vowels[0] = 'a';
vowels[1] = 'e';
vowels[2] = 'i';
vowels[3] = 'o';
vowels[4] = 'u';
Console.WriteLine(vowels[1]);
// e
```

This prints “e” because array indexes start at `0`.

You can use a for loop statement to iterate through each element in the array.  
The for loop in this example cycles the integer `i` from `0` to `4`:

```cs
for(int i = 0; i < vowels.Length; i++)
{
    Console.Write(vowels[i]); // aeiou
}
```

The Length property of an array returns the number of elements in the array.

After an array has been created,  
You cannot change its length.

The `System.Collection` namespace and subnamespaces provide higher-level data structures,  
Such as dynamically sized arrays and dictionaries.

An array _initialization expression_ lets you declare and populate an array in a single step:

```cs
var vowels = new char[] {'a','e','i','o','u'};
```

Or simply:

```cs
char[] vowels = {'a','e','i','o','u'};
```

Or:

```cs
char[] vowels = ['a','e','i','o','u'];
```

All arrays inherit from the `System.Array` class,  
Providing common services for all arrays.

These members include methods to get and set elements regardless of the array type.

## Default Element Initialization

Creating an array always preinitializes the elements with default values.  
The default value for a type is the result of a bitwise zeroing of memory.

For example,  
Consider creating an array of integers.  
Because `int` is a value type,  
This allocates 1,000 integers in one contiguous block of memory.  
The default value for each element will be `0`:

```cs
var a = new int[1000];
Console.Write(a[123]); // 0
```

### Value Types Versus Reference Types

Whether an array element type is a value type or a reference type has important performance implications.

When the element type is a value type,  
Each element value is allocated as part of the array,  
As shown here:

```cs
var a = new Point[1000];
var x = a[500].X; // 0

public struct Point
{
    public int X, Y;
}
```

Had Point been a class,  
Creating the array would have merely allocated 1,000 null references:

```cs
var a = new Point[1000];
var x = a[500].X; // Runtime error, NullReferenceException

public struct Point
{
    public int X, Y;
}
```

To avoid this error,  
We must explicitly instantiate 1,000 Points after instantiating the array:

```cs
var a = new Point[1000];

for(int i = 0; i < a.Length; i++) // Iterate i from 0 to 999
{
    a[i] = new Point(); // Set array element i with new point
}
```

An array itself is always a reference type object,  
Regardless of the element type.

For instance,  
The following is legal:

```cs
int[] a = null;
```
