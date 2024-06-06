---
sidebar_position: 2
---

# Ports & Adapters

## What is Ports & Adapters Pattern?

The ports & adapters architecture addresses the shortcomings of the layered architecture,  
And is a better fit for implementation of more complex business logic.

Interestingly, both patterns are quite similar.  
Let’s refactor the layered architecture into ports & adapters:

- ### Terminology

  Essentially, both the presentation layer and data access layer represent integration with external components:  
  Databases, external services, and user interface frameworks.

  These technical implementation details do not reflect the system’s business logic;  
  So, let’s unify all such infrastructural concerns into a single **Infrastructure Layer**.

- ### Dependency Inversion Principle

  The dependency inversion principle (DIP),  
  States that high-level modules,  
  Which implement the business logic,  
  Should not depend on low-level modules.

  However, that’s precisely what happens in the traditional layered architecture.  
  The business logic layer depends on the infrastructure layer.  
  To conform with the DIP,  
  Let’s reverse the relationship.

  Instead of being sandwiched between the technological concerns,  
  Now the business logic layer takes the central role.  
  It doesn’t depend on any of the system’s infrastructural components.

- ### Application Layer

  Finally, let’s add an application layer as a facade for the system’s public interface.  
  As the service layer in the layered architecture,

  It describes all the operations exposed by the system,  
  And orchestrates the system’s business logic for executing them.

The result is the ports & adapters architectural pattern.

The business logic doesn’t depend on any of the underlying layers,  
As required for implementing the domain model and event-sourced domain model patterns.

Why is this pattern called ports & adapters?  
To answer this question,  
Let’s see how the infrastructural components are integrated with the business logic.

## Integration of Infrastructural Components

The core goal of the ports & adapters architecture is,  
To decouple the system’s business logic,  
From its infrastructural components.

Instead of referencing and calling the infrastructural components directly,  
The business logic layer defines **Ports**,  
That have to be implemented by the infrastructure layer.

The infrastructure layer implements **Adapters**:  
Concrete implementations of the ports interfaces for working with different technologies.

The abstract ports are resolved into concrete adapters in the infrastructure layer,  
Either through dependency injection or by bootstrapping.

For example,  
Here is a possible port definition and a concrete adapter for a message bus:

```cs
namespace App.BusinessLogicLayer
{
    public interface IMessaging
    {
        void Publish(Message payload);
        void Subscribe(Message type, Action callback);
    }
}
```

```cs
namespace App.Infrastructure.Adapters
{
    public class SQSBus: IMessaging
    {
    }
}
```

## Variants

The ports & adapters architecture is also known as hexagonal architecture, onion architecture, and clean architecture.

All of these patterns are based on the same design principles,  
Have the same components,  
And have the same relationships between them.

But as in the case of the layered architecture,  
The terminology may differ:

- Application Layer = Service Layer = Use Case Layer
- Business Logic Layer = Domain Layer = Core Layer

Despite that, these patterns can be mistakenly treated as conceptually different.  
That’s just another example of the importance of a ubiquitous language.

## When to Use Ports & Adapters?

The decoupling of the business logic from all technological concerns,  
Makes the ports & adapters architecture a perfect fit for business logic implemented with the domain model pattern.

## References

- Learning Domain-Driven Design - Vladik Khononov - O'Reilly
