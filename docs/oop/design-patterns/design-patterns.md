---
sidebar_position: 2
---

# Design Patterns

## What are Design Patterns?

Design Patterns help you build flexible, reusable, and maintainable applications.

## How to Use Design Patterns?

The best way to use patterns is to load your brain with them,  
And then recognize places in your designs and existing applications where you can apply them.

:::tip Just another reminder
In design patterns, the phrase “implement an interface”  
does NOT always mean “write a class that implements a Java interface,  
by using the ‘implements' keyword in the class declaration.”

In the general use of the phrase, a concrete class implementing a method from a supertype  
(which could be a abstract class OR interface) is still considered to be “implementing the interface” of that supertype.
:::

## OO Patterns

### Strategy

Defines a family of algorithms, encapsulates each one, and makes them interchangeable.  
Strategy lets the algorithm vary independently from clients that use it.

### Observer

Defines a one-to-many dependency between objects so that when one object changes state,  
All of its dependents are notified and updated automatically.

### Decorator

Attach additional responsibilities to an object dynamically.  
Decorator provide a flexible alternative to subclassing for extending functionality.

### Factory Method

Defines an interface for creating an object, but let's subclasses decide which class to instantiate.  
Factory Method lets a class defer instantiation to subclasses.

### Abstract Factory

Provides an interface for creating families of related or dependent objects without specifying their concrete classes.

### Singleton

Ensures a class has only one instance, and provides a global point of access to it.

### Command

Encapsulates a request as an object,  
Thereby letting you parameterize clients with different requests, queue or log requests,  
And support undoable operations.

### Adapter

Converts the interface of a class into another interface the clients expect.  
Adapter lets classes work together that couldn’t otherwise because of incompatible interfaces.

### Facade

Provides a unified interface to a set of interfaces in a subsystem.  
Facade defines a higher-level interface that makes the subsystem easier to use.

### Template Method

Define the skeleton of an algorithm in an operation, deferring some steps to subclasses.  
Template Method lets subclasses redefine certain steps of an algorithm without changing the algorithm's structure.

### Iterator

Provide a way to access the elements of aggregate object sequentially without exposing it's underlying representation.

### Composite

Compose objects into tree structures to represent part-whole hierarchies.  
Composite lets clients treat individual objects and composites of objects uniformly.

### State

Allows an object to alter its behavior when its internal state changes.  
The object will appear to change its class.

## References

- Head First Design Patterns 2nd Edition - Elisabeth Robson, Eric Freeman - O'Reilly
