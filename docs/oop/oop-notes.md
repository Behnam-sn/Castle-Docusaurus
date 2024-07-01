# OOP Notes

## What is OOP?

Object-oriented programming (OOP) is a programming paradigm based on the concept of objects.

Which can contain data and code:  
Data in the form of fields (often known as attributes or properties),  
And code in the form of procedures (often known as methods).

In OOP, computer programs are designed by making them out of objects that interact with one another.

## Features

Object-oriented programming uses objects,  
But not all of the associated techniques and structures are supported directly in languages that claim to support OOP.

The features listed below are common among languages considered to be strongly object-oriented,  
Or multi-paradigm with OOP support, with notable exceptions mentioned.

:::note
Critical comparison of OOP to other technologies, relational in particular, is difficult,  
Because of lack of an agreed-upon and rigorous definition of OOP.
:::

### Objects

An object is a data structure or abstract data type,  
Containing:

- Fields  
  State variables containing data.  
  Fields may also be known as members, attributes, or properties.
- Methods  
  subroutines or procedures defining the object's behavior in code.

Objects are typically stored as contiguous regions of memory.

Objects are accessed somewhat like variables with complex internal structures,

And in many languages are effectively pointers,  
Serving as actual references to a single instance of said object in memory,  
Within a heap or stack.

Objects sometimes correspond to things found in the real world.  
For example, a graphics program may have objects such as "circle", "square", and "menu".  
An online shopping system might have objects such as "shopping cart", "customer", and "product".

Sometimes objects represent more abstract entities,  
Like an object that represents an open file,  
Or an object that provides the service of translating measurements from U.S. customary to metric.

:::tip
Objects can contain other objects in their instance variables;  
This is known as object composition.
:::

### Inheritance

OOP languages are diverse,  
But typically OOP languages allow inheritance,  
For code reuse and extensibility,  
In the form of either classes or prototypes.

These forms of inheritance are significantly different,  
But analogous terminology is used to define the concepts of **Object** and **Instance**.

#### Class-Based

In class-based programming,  
each object is required to be an instance of a particular **Class**.

The class defines the data format or type  
(including member variables and their types)  
and available procedures (class methods or member functions) for a given type or class of object.

Objects are created by calling a special type of method in the class known as a _constructor_.

Classes may inherit from other classes,  
So they are arranged in a hierarchy that represents "is-a-type-of" relationships.  
For example, Employee class might inherit from Person class.

All the data and methods available to the parent class,  
Also appear in the child class with the same names.

Depending on the definition of the language,  
Subclasses may or may not be able to override the methods defined by superclasses.

Multiple inheritance is allowed in some languages,  
Though this can make resolving overrides complicated.

#### Prototype-Based

In contrast, in prototype-based programming,  
Objects are the primary entities.

Generally, the concept of a "class" does not even exist.  
Rather, the prototype or parent of an object is just another object to which the object is linked.

An object may have multiple or no parents,  
But in the most popular prototype-based language, Javascript,  
Every object has one and only one prototype link.

New objects can be created based on already existing objects chosen as their prototype.

Unlike class-based programming,  
In prototype-based languages is possible to define attributes and methods not shared with other objects.

#### Absence

Some languages like Go do not support inheritance at all.  
Go states that it is object-oriented,  
And Bjarne Stroustrup, author of C++, has stated that it is possible to do OOP without inheritance.

The principle of "composition over inheritance" advocates implementing has-a relationships using composition instead of inheritance.  
For example,  
Instead of inheriting from class Person,  
class Employee could give each Employee object an internal Person object,  
Which it then has the opportunity to hide from external code even if class Person has many public attributes or methods.

Delegation is another language feature that can be used as an alternative to inheritance.

### Dynamic Dispatch

It is the responsibility of the object,  
Not any external code,  
To select the procedural code to execute in response to a method call,  
Typically by looking up the method at run time in a table associated with the object.

This feature is known as dynamic dispatch.

Dispatch interacts with inheritance;  
If a method is not present in a given object or class,  
The dispatch is delegated to its parent object or class, and so on, going up the chain of inheritance.

### Data abstraction and encapsulation

Data abstraction is a design pattern in which data are visible only to semantically related functions, to prevent misuse. The success of data abstraction leads to frequent incorporation of data hiding as a design principle in object-oriented and pure functional programming. Similarly, encapsulation prevents external code from being concerned with the internal workings of an object. This facilitates code refactoring, for example allowing the author of the class to change how objects of that class represent their data internally without changing any external code (as long as "public" method calls work the same way). It also encourages programmers to put all the code that is concerned with a certain set of data in the same class, which organizes it for easy comprehension by other programmers. Encapsulation is a technique that encourages decoupling.

In object oriented programming, objects provide a layer which can be used to separate internal from external code and implement abstraction and encapsulation. External code can only use an object by calling a specific instance method with a certain set of input parameters, reading an instance variable, or writing to an instance variable. A program may create many instances of objects as it runs, which operate independently. This technique, it is claimed, allows easy re-use of the same procedures and data definitions for different sets of data, in addition to potentially mirroring real-world relationships intuitively. Rather than utilizing database tables and programming subroutines, the developer utilizes objects the user may be more familiar with: objects from their application domain.

If a class does not allow calling code to access internal object data and permits access through methods only, this is also a form of information hiding. Some languages (Java, for example) let classes enforce access restrictions explicitly, for example, denoting internal data with the private keyword and designating methods intended for use by code outside the class with the public keyword.[43] Methods may also be designed public, private, or intermediate levels such as protected (which allows access from the same class and its subclasses, but not objects of a different class).[43] In other languages (like Python) this is enforced only by convention (for example, private methods may have names that start with an underscore). In C#, Swift & Kotlin languages, internal keyword permits access only to files present in the same assembly, package, or module as that of the class.

### Polymorphism

Subtyping – a form of polymorphism – is when calling code can be independent of which class in the supported hierarchy it is operating on – the parent class or one of its descendants. Meanwhile, the same operation name among objects in an inheritance hierarchy may behave differently.

For example, objects of the type Circle and Square are derived from a common class called Shape. The Draw function for each type of Shape implements what is necessary to draw itself while calling code can remain indifferent to the particular type of Shape being drawn.

This is another type of abstraction that simplifies code external to the class hierarchy and enables strong separation of concerns.

## References

- [en.wikipedia.org/wiki/Object-oriented_programming](https://en.wikipedia.org/wiki/Object-oriented_programming)

## OOP Notes 2

Object-oriented programming is about modeling a system as a collection of objects,  
Where each object represents some particular aspect of the system.

Objects contain both functions (or methods) and data.

An object provides a public interface to other code that wants to use it,  
But maintains its own private, internal state;  
Other parts of the system don't have to care about what is going on inside the object.

### Classes and instances

When we model a problem in terms of objects in OOP, we create abstract definitions representing the types of objects we want to have in our system. For example, if we were modeling a school, we might want to have objects representing professors. Every professor has some properties in common: they all have a name and a subject that they teach. Additionally, every professor can do certain things: they can all grade a paper and they can introduce themselves to their students at the start of the year, for example.

So Professor could be a class in our system. The definition of the class lists the data and methods that every professor has.

In pseudo-code, a Professor class could be written like this:

https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Objects/Object-oriented_programming
https://www.techtarget.com/searchapparchitecture/definition/object-oriented-programming-OOP#:~:text=Object%2Doriented%20programming%20(OOP)%20is%20a%20computer%20programming%20model,has%20unique%20attributes%20and%20behavior.
https://www.spiceworks.com/tech/devops/articles/object-oriented-programming/
https://www.educative.io/blog/object-oriented-programming
