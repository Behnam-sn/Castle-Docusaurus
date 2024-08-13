# Collections

.NET provides a standard set of types for storing and managing collections of objects.

These include resizable lists, linked lists, and sorted and unsorted dictionaries, as well as arrays.

Of these, only arrays form part of the C# language;

The remaining collections are just classes you instantiate like any other.

We can divide the types in the .NET BCL for collections into the following categories:

- Interfaces that define standard collection protocols
- Ready-to-use collection classes (lists, dictionaries, etc.)
- Base classes for writing application-specific collections

The collection namespaces are as follows:

| Namespace                      | Contains                                      |
| ------------------------------ | --------------------------------------------- |
| System.Collections             | Non-generic collection classes and interfaces |
| System.Collections.Specialized | Strongly typed non-generic collection classes |
| System.Collections.Generic     | Generic collection classes and interfaces     |
| System.Collections.ObjectModel | Proxies and bases for custom collections      |
| System.Collections.Concurrent  | Thread-safe collections                       |

## Enumeration

In computing, there are many different kinds of collections,  
Ranging from simple data structures such as arrays or linked lists,  
To more complex ones such as red/black trees and hash tables.

Although the internal implementation and external characteristics of these data structures vary widely,  
The ability to traverse the contents of the collection is an almost universal need.

The .NET BCL supports this need,  
Via a pair of interfaces (IEnumerable, IEnumerator, and their generic counterparts),  
That allow different data structures to expose a common traversal API.

### IEnumerable and IEnumerator

The `IEnumerator` interface defines the basic low-level protocol,  
By which elements in a collection are traversed (or enumerated) in a forward-only manner.

Its declaration is as follows:

```cs
public interface IEnumerator
{
    bool MoveNext();
    object Current { get; }
    void Reset();
}
```

`MoveNext` advances the current element or “cursor” to the next position,  
Returning false if there are no more elements in the collection.

`Current` returns the element at the current position.  
(Usually cast from object to a more specific type)

`MoveNext` must be called before retrieving the first element,  
This is to allow for an empty collection.

The `Reset` method, if implemented, moves back to the start,  
Allowing the collection to be enumerated again.

`Reset` exists mainly for Component Object Model (COM) interoperability;  
calling it directly is generally avoided,  
Because it’s not universally supported.  
And is unnecessary in that it’s usually just as easy to instantiate a new enumerator.

Collections do not usually implement enumerators;  
Instead, they provide enumerators, via the interface `IEnumerable`:

```cs
public interface IEnumerable
{
    IEnumerator GetEnumerator();
}
```

By defining a single method retuning an enumerator,  
`IEnumerable` provides flexibility in that the iteration logic can be farmed out to another class.

Moreover, it means that several consumers can enumerate the collection at once,  
Without interfering with one another.

You can think of `IEnumerable` as `IEnumerator` Provider,  
And it is the most basic interface that collection classes implement.

The following example illustrates low-level use of `IEnumerable` and `IEnumerator`:

```cs
var s = "Hello";
// Because string implements IEnumerable, we can call GetEnumerator():
var enumerator = s.GetEnumerator();
while (enumerator.MoveNext())
{
    var c = (char)enumerator.Current;
    Console.Write(c + ".");
}
// Output: H.e.l.l.o.
```

However,  
It’s rare to call methods on enumerators directly in this manner,  
Because C# provides a syntactic shortcut:  
The `foreach` statement.

Here’s the same example rewritten using `foreach`:

```cs
var s = "Hello";
// The String class implements IEnumerable
foreach (var c in s)
{
    Console.Write (c + ".");
}
// Output: H.e.l.l.o.
```

### IEnumerable\<T\> and IEnumerator\<T\>

`IEnumerator` and `IEnumerable` are nearly always implemented in conjunction with their extended generic versions:

```cs
public interface IEnumerator<T> : IEnumerator, IDisposable
{
    T Current { get; }
}

public interface IEnumerable<T> : IEnumerable
{
    IEnumerator<T> GetEnumerator();
}
```

By defining a typed version of `Current` and `GetEnumerator`,  
These interfaces strengthen static type safety,  
Avoid the overhead of boxing with value-type elements,  
And are more convenient to the consumer.

Arrays automatically implement `IEnumerable<T>`,  
Where `T` is the member type of the array.

Thanks to the improved static type safety,  
Calling the following method with an array of characters will generate a compile-time error:

```cs
void Test (IEnumerable<int> numbers)
{
    ...
}
```

It’s a standard practice for collection classes to publicly expose `IEnumerable<T>`,  
While “hiding” the non-generic `IEnumerable` through explicit interface implementation.

This is so that if you directly call `GetEnumerator()`,  
You get back the type-safe generic `IEnumerator<T>`.

There are times when this rule is broken for reasons of backward compatibility,  
Generics did not exist prior to C# 2.0.

A good example is arrays,
These must return the non-generic (the nice way of putting it is “classic”) `IEnumerator`,  
To avoid breaking earlier code.

To get a generic `IEnumerator<T>`,  
You must cast to expose the explicit interface:

```cs
int[] data = { 1, 2, 3 };
// Type of enumeratorA is IEnumerable
var enumeratorA = data.GetEnumerator();
// Type of enumeratorB is IEnumerable<int>
var enumeratorB = ((IEnumerable<int>)data).GetEnumerator();
```

Fortunately,  
You rarely need to write this sort of code,  
Thanks to the `foreach` statement.

#### IEnumerable\<T\> and IDisposable

`IEnumerator<T>` inherits from `IDisposable`.

This allows enumerators to hold references to resources such as database connections,
And ensure that those resources are released when enumeration is complete (or abandoned partway through).  
The `foreach` statement recognizes this detail and translates the following:

```cs
foreach (var element in somethingEnumerable)
{
    ...
}
```

into the logical equivalent of this:

```cs
using (var enumerator = somethingEnumerable.GetEnumerator())
{
    while (enumerator.MoveNext())
    {
        var element = enumerator.Current;
    }
}
```
