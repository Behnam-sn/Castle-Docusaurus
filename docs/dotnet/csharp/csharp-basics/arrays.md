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

## Indices

Indices let you refer to elements relative to the end of an array,  
With the `^` operator.

`^1` refers to the last element,  
`^2` refers to the second-to-last element,  
And so on:

```cs
var vowels = new char[] {'a','e','i','o','u'};
var lastElement = vowels[^1];  // 'u'
var secondToLast = vowels[^2]; // 'o'
```

:::note
`^0` equals the length of the array,  
So `vowels[^0]` generates an error.
:::

C# implements indices with the help of the `Index` type,  
So you can also do the following:

```cs
Index first = 0;
Index last = ^1;
var firstElement = vowels[first]; // 'a'
var lastElement = vowels[last]; // 'u'
```

## Ranges

Ranges let you _slice_ an array by using the `..` operator:

```cs
var firstTwo = vowels[..2]; // 'a', 'e'
var lastThree = vowels[2..]; // 'i', 'o', 'u'
var middleOne = vowels[2..3]; // 'i'
```

The second number in the range is exclusive,  
So `..2` returns the elements before `vowels[2]`.

You can also use the `^` symbol in ranges.  
The following returns the last two characters:

```cs
var lastTwo = vowels[^2..]; // 'o', 'u'
```

C# implements ranges with the help of the `Range` type,  
So you can also do the following:

```cs
Range firstTwoRange = 0..2;
var firstTwo = vowels[firstTwoRange]; // 'a', 'e'
```

## Multidimensional Arrays

Multidimensional arrays come in two varieties:

### Rectangular Arrays

Rectangular arrays represent an n-dimensional block of memory.

Rectangular arrays are declared using commas to separate each dimension.  
The following declares a rectangular two-dimensional array for which the dimensions are 3 by 3:

```cs
int[,] matrix = new int[3,3];
```

The `GetLength` method of an array returns the length for a given dimension (starting at 0):

```cs
for(var i = 0; i < matrix.GetLength(0); i++)
{
    for(var j = 0; j < matrix.GetLength(1); j++)
    {
        matrix[i,j] = i * 3 + j;
    }
}
```

You can initialize a rectangular array with explicit values.  
The following code creates an array identical to the previous example:

```cs
var matrix = new int[,]
{
    { 0, 1, 2 },
    { 3, 4, 5 },
    { 6, 7, 8 }
};

```

### Jagged Arrays

Jagged arrays are arrays of arrays.

Jagged arrays are declared using successive square brackets to represent each dimension.  
Here is an example of declaring a jagged two-dimensional array,  
For which the outermost dimension is 3:

```cs
int[][] matrix = new int[3][];
```

The inner dimensions aren’t specified in the declaration because,  
Unlike a rectangular array,  
Each inner array can be an arbitrary length.

Each inner array is implicitly initialized to `null` rather than an empty array.  
You must manually create each inner array:

```cs
for(var i = 0; i < matrix.Length; i++)
{
    matrix[i] = new int[3]; // Create inner array
    for (var j = 0; j < matrix[i].Length; j++)
    {
        matrix[i][j] = i * 3 + j;
    }
}

```

You can initialize a jagged array with explicit values.  
The following code creates an array identical to the previous example,  
With an additional element at the end:

```cs
var matrix = new int[][]
{
    new int[] { 0, 1, 2 },
    new int[] { 3, 4, 5 },
    new int[] { 6, 7, 8, 9 }
};
```

## Bounds Checking

All array indexing is bounds checked by the runtime.

An `IndexOutOfRangeException` is thrown if you use an invalid index:

```cs
var arr = new int[3];
arr[3] = 1; // IndexOutOfRangeException thrown
```

Array bounds checking is necessary for type safety and simplifies debugging

## References

- C# 12 in a Nutshell - Joseph Albahari - OReilly
