# Syntax

C# syntax is inspired by C and C++ syntax.

Lets describe C#’s elements of syntax,  
Using the following program:

```cs
using System;

int x = 12 * 30;
Console.WriteLine(x);
```

## Identifiers

Identifiers are names that programmers choose for their classes, methods, variables, and so on.

Here are the identifiers in our example program,  
In the order in which they appear:

```console
System
x
Console
WriteLine
```

An identifier must be a whole word,  
Essentially made up of Unicode characters starting with a letter or underscore.

C# identifiers are case sensitive.

By convention, parameters, local variables, and private fields should be in camel case (e.g., myVariable),  
And all other identifiers should be in Pascal case (e.g., MyMethod).

## Keywords

Keywords are names that mean something special to the compiler.

There are two keywords in our example program:  
`using` and `int`.

Most keywords are reserved,  
Which means that you can’t use them as identifiers.

Here is the full list of C# reserved keywords:

- abstract
- as
- base
- bool
- break
- byte
- case
- catch
- char
- checked
- class
- const
- continue
- decimal
- default
- delegate
- do
- double
- else
- enum
- event
- explicit
- extern
- false
- finally
- fixed
- float
- for
- foreach
- goto
- if
- implicit
- in
- int
- interface
- internal
- is
- lock
- long
- namespace
- new
- null
- object
- operator
- out
- override
- params
- private
- protected
- public
- readonly
- record
- ref
- return
- sbyte
- sealed
- short
- sizeof
- stackalloc
- static
- string
- struct
- switch
- this
- throw
- true
- try
- typeof
- uint
- ulong
- unchecked
- unsafe
- ushort
- using
- virtual
- void
- volatile
- while

If you really want to use an identifier that clashes with a reserved keyword,  
You can do so by qualifying it with the `@` prefix.

For instance:

```cs
int using = 123;  // Illegal
int @using = 123; // Legal
```

The `@` symbol doesn’t form part of the identifier itself.  
So, `@myVariable` is the same as `myVariable`.

### Contextual keywords

Some keywords are contextual,  
Meaning that you also can use them as identifiers without an `@` symbol:

- add
- alias
- and
- ascending
- async
- await
- by
- descending
- dynamic
- equals
- file
- from
- get
- global
- group
- init
- into
- join
- let
- managed
- nameof
- nint
- not
- notnull
- nuint
- on
- or
- orderby
- partial
- remove
- required
- select
- set
- unmanaged
- value
- var
- with
- when
- where
- yield

With contextual keywords,  
Ambiguity cannot arise within the context in which they are used.

## Literals

Literals are primitive pieces of data lexically embedded into the program.  
The literals we used in our example program are `12` and `30`.

## Punctuators

Punctuators help demarcate the structure of the program.  
An example is the semicolon, which terminates a statement.

Statements can wrap multiple lines:

```cs
Console.WriteLine
(1 + 2 + 3 + 4 + 5 + 6 + 7 + 8 + 9 + 10);
```

## Operators

An operator transforms and combines expressions.  
Most operators in C# are denoted with a symbol,  
Such as the multiplication operator, `*`.

These are the operators we used in our example program:

```cs
=
*
.
()
```

A period denotes a member of something (or a decimal point with numeric literals).

Parentheses are used when declaring or calling a method;  
Empty parentheses are used when the method accepts no arguments.

An equals sign performs assignment.

## Comments

C# offers two different styles of source-code documentation:

- ### Single-line Comments

  A single-line comment begins with a double forward slash and continues until the end of the line;  
  For example:

  ```cs
  var x = 3; // Comment about assigning 3 to x
  ```

- ### Multiline Comments

  A multiline comment begins with `/*` and ends with `*/`;  
  For example:

  ```cs
  var x = 3; /* This is a comment that
              spans two lines */
  ```

Comments can embed XML documentation tags.

## References

- C# 12 in a Nutshell - Joseph Albahari - OReilly
