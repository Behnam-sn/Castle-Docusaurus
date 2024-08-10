# C# Language

C# is a general-purpose, type-safe, object-oriented programming language.

The goal of the language is programmer productivity.

To this end, C# balances simplicity, expressiveness, and performance.

C# is a rich implementation of the object-orientation paradigm,  
which includes encapsulation, inheritance, and polymorphism.

Encapsulation means creating a boundary around an object,  
To separate its external (public) behavior from its internal (private) implementation details.

Following are the distinctive features of C# from an object-oriented perspective:

## Unified type system

The fundamental building block in C# is an encapsulated unit of data and functions called a `type`.

C# has a _unified type_ system in which all types ultimately share a common base type.

This means that all types,  
Whether they represent business objects or are primitive types such as numbers,  
Share the same basic functionality.

For example, an instance of any type can be converted to a string by calling its `ToString` method.

## Classes and interfaces

In a traditional object-oriented paradigm,  
The only kind of type is a class.

In C#, there are several other kinds of types,  
One of which is an interface.

An interface is like a class that cannot hold data.

This means that it can define only behavior (and not state),  
Which allows for multiple inheritance as well as a separation between specification and implementation.

## Properties, methods, and events

In the pure object-oriented paradigm, all functions are methods.

In C#, methods are only one kind of function member,  
Which also includes properties and events (there are others, too).

Properties are function members that encapsulate a piece of an object’s state,  
Such as a button’s color or a label’s text.

Events are function members that simplify acting on object state changes.

## functional programming paradigm

Although C# is primarily an object-oriented language,  
It also borrows from the functional programming paradigm, specifically:

### Functions can be treated as values

Using delegates,  
C# allows functions to be passed as values to and from other functions.

### C# supports patterns for purity

One of the core fundamentals of functional programming is avoiding the use of variables whose values change, in favor of declarative patterns.

C# has key features to help with those patterns,  
Including the ability to write unnamed functions on the fly,  
That “capture” variables (lambda expressions),  
And the ability to perform list or reactive programming via query expressions.

C# also provides records, which make it easy to write immutable (read-only) types.
