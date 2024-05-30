---
sidebar_position: 6
---

# Managing Complexity

## What is The Definition of Complexity?

As perviously mentioned,  
The aggregate and value object patterns were introduced as a means for tackling complexity in the implementation of business logic.

Let’s see the reasoning behind this.

In his book The Choice, business management guru Eliyahu M. Goldratt outlines a succinct yet powerful definition of system complexity.

According to Goldratt,  
When discussing the complexity of a system we are interested in evaluating the difficulty of controlling and predicting the system’s behavior.

These two aspects are reflected by the system’s degrees of freedom.

A system’s degrees of freedom are the data points needed to describe its state.

Consider the following two classes:

```cs
public class ClassA
{
    public int A { get; set; }
    public int B { get; set; }
    public int C { get; set; }
    public int D { get; set; }
    public int E { get; set; }
}

public class ClassB
{
    private int _a, _d;

    public int A
    {
        get => _a;
        set
        {
            _a = value;
            B = value / 2;
            C = value / 3;
        }
    }
    public int B { get; private set; }
    public int C { get; private set; }
    public int D
    {
        get => _d;
        set
        {
            _d = value;
            E = value * 2
        }
    }
    public int E { get; private set; }
}
```

At first glance, it seems that `ClassB` is much more complex than `ClassA`.  
It has the same number of variables, but on top of that, it implements additional calculations.  
Is it more complex than `ClassA`?

Let’s analyze both classes from the degrees-of-freedom perspective.  
How many data elements do you need to describe the state of `ClassA`?  
The answer is five: its five variables.  
Hence, `ClassA` has five degrees of freedom.

How many data elements do you need to describe the state of `ClassB`?  
If you look at the assignment logic for properties A and D, you will notice that the values of B, C, and E are functions of the values of A and D.  
If you know what A and D are, then you can deduce the values of the rest of the variables.  
Therefore, `ClassB` has only two degrees of freedom.  
You need only two values to describe its state.

Going back to the original question,  
Which class is more difficult in terms of controlling and predicting its behavior?  
The answer is the one with more degrees of freedom, or `ClassA`.

The invariants introduced in `ClassB` reduce its complexity.  
That’s what both aggregate and value object patterns do: encapsulate invariants and thus reduce complexity.

All the business logic related to the state of a value object is located in its boundaries.  
The same is true for aggregates.  
An aggregate can only be modified by its own methods.  
Its business logic encapsulates and protects business invariants, thus reducing the degrees of freedom.

Since the domain model pattern is applied only for subdomains with complex business logic,  
it’s safe to assume that these are core subdomains—the heart of the software.

## References

- Learning Domain-Driven Design - Vladik Khononov - O'Reilly
