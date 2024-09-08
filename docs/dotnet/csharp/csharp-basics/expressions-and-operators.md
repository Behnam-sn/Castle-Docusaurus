# Expressions and Operators

An _expression_ essentially denotes a value.

The simplest kinds of expressions are constants and variables.

Expressions can be transformed and combined using operators.

An _operator_ takes one or more input operands to output a new expression.

Here is an example of a constant expression:

```cs
12
```

We can use the `*` operator to combine two operands (the literal expressions `12` and `30`),  
As follows:

```cs
12 * 30
```

We can build complex expressions because an operand can itself be an expression,  
Such as the operand `(12 * 30)` in the following example:

```cs
1 + (12 * 30)
```

Operators in C# can be classed as unary, binary, or ternary,  
Depending on the number of operands they work on (one, two, or three).

The binary operators always use infix notation,  
In which the operator is placed between the two operands.
