# Variables

## What Is A Variable?

A variable represents a storage location,  
That has a modifiable value.

A variable can be a local variable, parameter, field, or array element.

## The Stack And The Heap

The stack and the heap are the places where variables reside.

Each has very different lifetime semantics.

### Stack

The stack is a block of memory,  
For storing local variables and parameters.

The stack logically grows and shrinks,  
As a method or function is entered and exited.

Consider the following method:

```cs
static int Factorial(int x)
{
    if(x == 0)
    {
        return 1;
    }

    return x * Factorial(x - 1);
}
```

This method is recursive,  
Meaning that it calls itself.

Each time the method is entered,  
A new `int` is allocated on the stack,  
And each time the method exits,  
The `int` is de-allocated.

### Heap

The heap is the memory in which objects (reference-type instances) reside.

Whenever a new object is created,  
It is allocated on the heap,  
And a reference to that object is returned.

During a program’s execution,  
The heap begins filling up as new objects are created.

The runtime has a garbage collector,  
And it will periodically de-allocates objects from the heap,  
So your program does not run out of memory.

An object is eligible for de-allocation as soon as it’s not referenced by anything that’s itself _alive_.

In the following example,  
We begin by creating a `StringBuilder` object,  
Referenced by the variable `ref1`,  
And then write out its content.

That `StringBuilder` object is then immediately eligible for garbage collection,  
Because nothing subsequently uses it.

Then, we create another `StringBuilder`,  
Referenced by variable `ref2`,  
And copy that reference to `ref3`.

Even though `ref2` is not used after that point,  
`ref3` keeps the same `StringBuilder` object alive,  
Ensuring that it doesn’t become eligible for collection until we’ve finished using `ref3`:

```cs
using System;
using System.Text;

var ref1 = new StringBuilder("object1");
Console.WriteLine(ref1);
// The StringBuilder referenced by ref1 is now eligible for GC.

var ref2 = new StringBuilder("object2");
var ref3 = ref2;
// The StringBuilder referenced by ref2 is NOT yet eligible for GC.
Console.WriteLine(ref3);
```

Value-type instances (and object references) live wherever the variable was declared.

If the instance was declared as a field within a class type,  
Or as an array element,  
That instance lives on the heap.

You can’t explicitly delete objects in C#, as you can in C++.  
An unreferenced object is eventually collected by the garbage collector.

The heap also stores static fields.  
Unlike objects allocated on the heap (which can be garbage-collected),  
These live until the process ends.
