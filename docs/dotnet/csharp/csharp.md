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

One of the core fundamentals of functional programming,  
Is avoiding the use of variables whose values change,  
In favor of declarative patterns.

C# has key features to help with those patterns,  
Including the ability to write unnamed functions on the fly,  
That “capture” variables (lambda expressions),  
And the ability to perform list or reactive programming via query expressions.

C# also provides records, which make it easy to write immutable (read-only) types.

## Type Safety

C# is primarily a type-safe language,  
Meaning that instances of types can interact only through protocols they define,  
Thereby ensuring each type’s internal consistency.

For instance,  
C# prevents you from interacting with a string type as though it were an integer type.

More specifically, C# supports _static typing_,  
Meaning that the language enforces type safety at compile time.  
This is in addition to type safety being enforced at runtime.

Static typing eliminates a large class of errors before a program is even run.

It shifts the burden away from runtime unit tests onto the compiler,  
To verify that all the types in a program fit together correctly.

This makes large programs much easier to manage, more predictable, and more robust.

Furthermore, static typing allows tools such as IntelliSense in Visual Studio to help you write a program because it knows for a given variable what type it is, and hence what methods you can call on that variable.

Such tools can also identify everywhere in your program that a variable, type, or method is used, allowing for reliable refactoring.

C# also allows parts of your code to be dynamically typed via the `dynamic` keyword.  
However, C# remains a predominantly statically typed language.

C# is also called a strongly typed language,  
Because its type rules are strictly enforced (whether statically or at runtime).

For instance,  
You cannot call a function that’s designed to accept an integer with a floating-point number,  
Unless you first explicitly convert the floating-point number to an integer.  
This helps prevent mistakes.

## Memory Management

C# relies on the runtime to perform automatic memory management.

The Common Language Runtime has a garbage collector,  
That executes as part of your program,  
Reclaiming memory for objects that are no longer referenced.

This frees programmers from explicitly de-allocating the memory for an object,  
Eliminating the problem of incorrect pointers encountered in languages such as C++.

C# does not eliminate pointers:  
It merely makes them unnecessary for most programming tasks.

For performance-critical hot-spots and interoperability,  
Pointers and explicit memory allocation is permitted in blocks that are marked unsafe.

## Platform Support

C# has runtimes that support the following platforms:

- Windows 7+ Desktop (for rich-client, web, server, and command-line applications)
- macOS (for web and command-line applications—and rich-client applications via Mac Catalyst)
- Linux (for web and command-line applications)
- Android and iOS (for mobile applications)
- Windows 10 devices (Xbox, Surface Hub, and HoloLens) via UWP

There is also a technology called Blazor that can compile C# to web assembly that runs in a browser.

## CLRs, BCLs, and Runtimes

Runtime support for C# programs consists of a _Common Language Runtime_ and a _Base Class Library_.

A runtime can also include a higher-level application layer,  
That contains libraries for developing rich-client, mobile, or web applications.

Different runtimes exist to allow for different kinds of applications, as well as different platforms.

### Common Language Runtime

A Common Language Runtime (CLR) provides essential runtime services,  
Such as automatic memory management and exception handling.

The word “common” refers to the fact that the same runtime can be shared by other managed programming languages,  
Such as F#, Visual Basic, and Managed C++.

C# is called a managed language,  
Because it compiles source code into managed code,  
Which is represented in Intermediate Language (IL).

The CLR converts the IL into the native code of the machine,  
such as X64 or X86, usually just prior to execution.  
This is referred to as Just-In-Time (JIT) compilation.

Ahead-of-time compilation is also available,  
To improve startup time with large assemblies or resource-constrained devices,  
And to satisfy iOS app store rules when developing mobile apps.

The container for managed code is called an assembly.

An assembly contains not only IL but also type information (metadata).

The presence of metadata allows assemblies to reference types in other assemblies without needing additional files.
