---
sidebar_position: 3
---

# Domain Model

## What is Domain Model Pattern?

<!-- > A domain model is an object model of the domain that incorporates both behavior and data.
> — Martin Fowler -->

The domain model pattern is intended to cope with cases of complex business logic.

Here, instead of CRUD interfaces,  
We deal with:  
Complicated state transitions,  
Business rules,  
And invariants (rules that have to be protected at all times).

## What Problem Domain Model Pattern is Trying to Solve?

Let’s assume we are implementing a help desk system.

Consider the following excerpt from the requirements,  
That describes the logic controlling the lifecycles of support tickets:

- Customers open support tickets describing issues they are facing.
- Both the customer and the support agent append messages.
- And all the correspondence is tracked by the support ticket.
- Each ticket has a priority: low, medium, high, or urgent.
- An agent should offer a solution within a set time limit (SLA),  
  That is based on the ticket’s priority.
- If the agent doesn’t reply within the SLA,  
  The customer can escalate the ticket to the agent’s manager.
- Escalation reduces the agent’s response time limit by 33%.
- If the agent didn’t open an escalated ticket within 50% of the response time limit,  
  It is automatically reassigned to a different agent.
- Tickets are automatically closed if the customer doesn’t reply to the agent’s questions within seven days.
- Escalated tickets cannot be closed automatically or by the agent,  
  Only by the customer or the agent’s manager.
- A customer can reopen a closed ticket only if it was closed in the past seven days.

These requirements form an entangled net of dependencies among the different rules,  
All affecting the support ticket’s lifecycle management logic.

This is not a CRUD data entry screen.

Attempting to implement this logic using active record objects,  
Will make it easy to duplicate the logic and corrupt the system’s state,  
By mis-implementing some of the business rules.

## What is Domain Model Pattern Solution?

Let’s look at the central domain model building blocks, or tactical patterns, offered by DDD:

- ### Value Objects

  Concepts of the business domain,  
  That can be identified exclusively by their values.

  Value objects do not require an explicit ID field.

  Since a change in one of the fields semantically creates a new value,  
  Value objects are immutable.

  Value objects model not only data, but behavior as well.  
  Methods manipulating the values and thus initializing new value objects.

- ### Entities

  An entity is the opposite of a value object.

- ### Aggregates

  A hierarchy of entities sharing a transactional boundary.

  All of the data included in an aggregate’s boundary,  
  Has to be strongly consistent,  
  To implement its business logic.

  The state of the aggregate,  
  And its internal objects,  
  Can only be modified through its public interface,  
  By executing the aggregate’s commands.

- ### Domain Events

  An aggregate can communicate with external entities,  
  By publishing domain events.

  Domain events are messages,  
  Describing important business events,  
  In the aggregate’s lifecycle.

  Other components can subscribe to the events,  
  And use them to trigger the execution of business logic.

- ### Domain Services

  A domain service is a stateless object,  
  That hosts business logic that naturally doesn’t belong to any of,  
  The domain model’s aggregates or value objects.

:::note
All of these patterns share a common theme:  
They put the business logic first.
:::

## How the Domain Model Addresses Different Design Concerns?

### Complexity

The domain’s business logic is already inherently complex,  
So the objects used for modeling it,  
Should not introduce any additional accidental complexities.

The model should be devoid of any infrastructural or technological concerns,  
Such as implementing calls to databases or other external components of the system.

This restriction requires the model’s objects to be _plain old objects_,  
Objects implementing business logic without relying on (or directly incorporating),  
Any infrastructural components or frameworks.

### Ubiquitous Language

The emphasis on business logic instead of technical concerns,  
Makes it easier for the domain model’s objects,  
To follow the terminology of the bounded context’s ubiquitous language.

In other words,  
This pattern allows the code to speak the ubiquitous language,  
And to follow the domain experts mental models.

## References

- Learning Domain-Driven Design - Vladik Khononov - O'Reilly
