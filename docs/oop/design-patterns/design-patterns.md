---
sidebar_position: 2
---

# Design Patterns

## What are Design Patterns?

A Pattern is a solution to a problem in a context.  
Design Pattern gives you a solution to a common recurring design problem.  
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

Creational:
Abstract Factory
Factory Method
Singleton
Builder
Prototype

Behavioral:
Template Method
State
Strategy
Command
Observer
Iterator
Visitor
Mediator
Memento
Interpreter
Chain of Responsibility

Structural:
Proxy
Decorator
Composite
Facade
Adapter
Bridge
Flyweight

## Creational Patterns

### Factory Method

Defines an interface for creating an object, but let's subclasses decide which class to instantiate.  
Factory Method lets a class defer instantiation to subclasses.

### Abstract Factory

Provides an interface for creating families of related or dependent objects without specifying their concrete classes.

### Builder

Use the Builder Pattern to encapsulate the construction of a product and allow it to be constructed in steps.

### Singleton

Ensures a class has only one instance, and provides a global point of access to it.

### Prototype

Use the Prototype Pattern when creating an instance of a given class is either expensive or complicated.

## Structural Patterns

### Adapter

Converts the interface of a class into another interface the clients expect.  
Adapter lets classes work together that couldn’t otherwise because of incompatible interfaces.

### Facade

Provides a unified interface to a set of interfaces in a subsystem.  
Facade defines a higher-level interface that makes the subsystem easier to use.

### Bridge

Use the Bridge Pattern to vary not only your implementations, but also your abstractions.

### Composite

Compose objects into tree structures to represent part-whole hierarchies.  
Composite lets clients treat individual objects and composites of objects uniformly.

### Decorator

Attach additional responsibilities to an object dynamically.  
Decorator provide a flexible alternative to subclassing for extending functionality.

### Flyweight

Use the Flyweight Pattern when one instance of a class can be used to provide many virtual instances.

### Proxy

Provides a surrogate or placeholder for another object to control access to it.  
Use the Proxy Pattern to create a representative object that controls access to another object,  
Which may be remote, expensive to create, or in need of securing.

## Behavioral Patterns

### Iterator

Provide a way to access the elements of aggregate object sequentially without exposing it's underlying representation.

### Strategy

Defines a family of algorithms, encapsulates each one, and makes them interchangeable.  
Strategy lets the algorithm vary independently from clients that use it.

### State

Allows an object to alter its behavior when its internal state changes.  
The object will appear to change its class.

### Observer

Defines a one-to-many dependency between objects so that when one object changes state,  
All of its dependents are notified and updated automatically.

### Command

Encapsulates a request as an object,  
Thereby letting you parameterize clients with different requests, queue or log requests, and support undoable operations.

### Template Method

Define the skeleton of an algorithm in an operation, deferring some steps to subclasses.  
Template Method lets subclasses redefine certain steps of an algorithm without changing the algorithm's structure.

### Chain of Responsibility

Use the Chain of Responsibility Pattern when you want to give more than one object a chance to handle a request.

### Interpreter

Use the Interpreter Pattern to build an interpreter for a language.

### Mediator

Use the Mediator Pattern to centralize complex communications and control between related objects.

### Memento

Use the Memento Pattern when you need to be able to return an object to one of its previous states;  
For instance, if your user requests an “undo.”

### Visitor

Use the Visitor Pattern when you want to add capabilities to a composite of objects and encapsulation is not important.

## Compound Patterns

A Compound Pattern combines two or more patterns into a solution that solves a recurring or general problem.

## References

- Head First Design Patterns 2nd Edition - Elisabeth Robson, Eric Freeman - O'Reilly
