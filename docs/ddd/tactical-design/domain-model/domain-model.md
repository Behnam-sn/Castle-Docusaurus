# Domain Model

## What is Domain Model Pattern?

> A domain model is an object model of the domain that incorporates both behavior and data.  
> — Martin Fowler

The domain model pattern is intended to cope with cases of complex business logic.  
Here, instead of CRUD interfaces,  
We deal with complicated state transitions,  
Business rules,  
And invariants: rules that have to be protected at all times.

## What Problem is Domain Model Pattern Trying to Solve?

Let’s assume we are implementing a help desk system.  
Consider the following excerpt from the requirements that describes the logic controlling the lifecycles of support tickets:

- Customers open support tickets describing issues they are facing.
- Both the customer and the support agent append messages.
- And all the correspondence is tracked by the support ticket.
- Each ticket has a priority: low, medium, high, or urgent.
- An agent should offer a solution within a set time limit (SLA) that is based on the ticket’s priority.
- If the agent doesn’t reply within the SLA, the customer can escalate the ticket to the agent’s manager.
- Escalation reduces the agent’s response time limit by 33%.
- If the agent didn’t open an escalated ticket within 50% of the response time limit,  
  It is automatically reassigned to a different agent.
- Tickets are automatically closed if the customer doesn’t reply to the agent’s questions within seven days.
- Escalated tickets cannot be closed automatically or by the agent, only by the customer or the agent’s manager.
- A customer can reopen a closed ticket only if it was closed in the past seven days.

These requirements form an entangled net of dependencies among the different rules,  
All affecting the support ticket’s lifecycle management logic.

This is not a CRUD data entry screen.  
Attempting to implement this logic using active record objects will make it easy to duplicate the logic and corrupt the system’s state by mis-implementing some of the business rules.

## What is Domain Model Pattern Solution?

some patterns.

Let’s see how the domain model addresses different design concerns:

### Complexity

The domain’s business logic is already inherently complex,  
So the objects used for modeling it should not introduce any additional accidental complexities.

The model should be devoid of any infrastructural or technological concerns,  
Such as implementing calls to databases or other external components of the system.

This restriction requires the model’s objects to be _plain old objects_,  
Objects implementing business logic without relying on or directly incorporating any infrastructural components or frameworks.

### Ubiquitous Language

The emphasis on business logic instead of technical concerns makes it easier for the domain model’s objects to follow the terminology of the bounded context’s ubiquitous language.

In other words, this pattern allows the code to “speak” the ubiquitous language and to follow the domain experts’ mental models.

## How to Implement Domain Model Pattern?

Let’s look at the central domain model building blocks, or tactical patterns, offered by DDD:

- ### Value Objects

  Concepts of the business domain that can be identified exclusively by their values,  
  And thus do not require an explicit ID field.  
  Since a change in one of the fields semantically creates a new value, value objects are immutable.

  Value objects model not only data, but behavior as well.  
  Methods manipulating the values and thus initializing new value objects.

- ### Entities

- ### Aggregates

  A hierarchy of entities sharing a transactional boundary.  
  All of the data included in an aggregate’s boundary has to be strongly consistent to implement its business logic.

  The state of the aggregate, and its internal objects,  
  Can only be modified through its public interface, by executing the aggregate’s commands.

- ### Domain Events

  An aggregate can communicate with external entities, by publishing domain events.  
  Domain events are messages describing important business events in the aggregate’s lifecycle.  
  Other components can subscribe to the events and use them to trigger the execution of business logic.

- ### Domain Services

  A stateless object that hosts business logic that naturally doesn’t belong to any of
  the domain model’s aggregates or value objects.

All of these patterns share a common theme:  
They put the business logic first.

## References

- Learning Domain-Driven Design - Vladik Khononov - O'Reilly
