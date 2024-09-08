# Null Operators

C# provides three operators to make it easier to work with nulls:

## Null-Coalescing Operator

The `??` operator is the null-coalescing operator.

It says:

_If the operand to the left is non-null, give it to me;_  
_Otherwise, give me another value._

For example:

```cs
var s1 = null;
var s2 = s1 ?? "nothing"; // s2 evaluates to "nothing"
```

If the lefthand expression is non-null,  
The righthand expression is never evaluated.

## Null-Coalescing Assignment Operator

The `??=` operator (introduced in C# 8),  
Is the null-coalescing assignment operator.

It says:

_If the operand to the left is null,_  
_Assign the right operand to the left operand._

Consider the following:

```cs
myVariable ??= someDefault;
```

This is equivalent to:

```cs
if (myVariable == null) myVariable = someDefault;
```

## Null-Conditional Operator

The `?.` operator is the null-conditional or “Elvis” operator (after the Elvis emoticon).

It allows you to call methods and access members just like the standard dot operator,  
Except that if the operand on the left is null,  
The expression evaluates to null instead of throwing a `NullReferenceException`:

```cs
System.Text.StringBuilder sb = null;
var s = sb?.ToString(); // No error; s instead evaluates to null
```

The last line is equivalent to the following:

```cs
var s = (sb == null ? null : sb.ToString());
```

Null-conditional expressions also work with indexers:

```cs
string[] words = null;
var word = words?[1]; // word is null
```

Upon encountering a null,  
The Elvis operator short-circuits the remainder of the expression.

In the following example,  
`s` evaluates to null,  
Even with a standard dot operator between `ToString()` and `ToUpper()`:

```cs
System.Text.StringBuilder sb = null;
var s = sb?.ToString().ToUpper(); // s evaluates to null without error
```

Repeated use of Elvis is necessary only if the operand immediately to its left might be null.  
The following expression is robust to both `x` being null and `x.y` being null:

```cs
x?.y?.z
```

It is equivalent to the following,  
Except that `x.y` is evaluated only once:

```cs
x == null
    ? null
    : (x.y == null ? null : x.y.z)
```

The final expression must be capable of accepting a null.  
The following is illegal:

```cs
System.Text.StringBuilder sb = null;
int length = sb?.ToString().Length; // Illegal : int cannot be null
```

You can also use the null-conditional operator to call a `void` method:

```cs
someObject?.SomeVoidMethod();
```

If `someObject` is null,  
This becomes a “no-operation” rather than throwing a `NullReferenceException`.

## References

- C# 12 in a Nutshell - Joseph Albahari - OReilly
