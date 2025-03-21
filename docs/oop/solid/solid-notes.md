# SOLID Notes

## What

The SOLID principles are 5 fundamental design principles,  
In object-oriented programming (OOP),  
That help create software that is more maintainable, scalable, and flexible.

They were introduced by Robert C. Martin (Uncle Bob),  
And are widely used in software engineering.

### SOLID Principles

- #### Single Responsibility Principle

  A class should have only one reason to change.

  - Each class should have one and only one responsibility.
  - Helps keep the code modular and easy to maintain.
  - Example: A User class should not handle logging;  
    That should be a separate Logger class.

- #### Open/Closed Principle

  Software entities (classes, modules, functions),  
  Should be open for extension but closed for modification.

  - You should be able to add new functionality without changing existing code.
  - Achieved using polymorphism and abstraction (e.g., interfaces, inheritance).
  - Example: Instead of modifying a `PaymentProcessor` class for each payment method,  
    Create a `PaymentMethod` interface and implement classes like `CreditCardPayment`, `PayPalPayment`, etc.

- #### Liskov Substitution Principle

  Subtypes must be substitutable for their base types,  
  Without altering the correctness of the program.

  - A subclass should be fully replaceable by its parent class without unexpected behavior.
  - Avoid breaking inheritance by ensuring consistency.
  - Example: If `Bird` has a `Fly()` method,  
    Then `Penguin : Bird` should not inherit `Fly()` because penguins can't fly.  
    Instead, introduce an `IFlyable` interface.

- #### Interface Segregation Principle

  A class should not be forced to implement interfaces it does not use.

  - Large interfaces should be split into smaller, more specific interfaces.
  - Avoid fat interfaces that require implementing unnecessary methods.
  - Example: Instead of one `IMachine` interface with `Print()`, `Scan()`, and `Fax()`,  
    Separate into `IPrinter`, `IScanner`, and `IFaxMachine`.

- #### Dependency Inversion Principle

  High-level modules should not depend on low-level modules.  
  Both should depend on abstractions.  
  Abstractions should not depend on details.  
  Details should depend on abstractions.

  - Use dependency injection and inversion of control (IoC).
  - Reduces tight coupling between modules.
  - Example: Instead of a `Service` class directly instantiating a `Database` class,  
    It should depend on an `IDatabase` interface,  
    Allowing flexibility in choosing different database implementations.

## Why Use SOLID?

- Easier Maintenance

  Changes in one part of the code do not break others.

- Scalability

  Software can be extended without modifying existing code.

- Readability & Reusability

  Code is cleaner and more modular.

- Testability

  Loose coupling makes unit testing easier.
