---
sidebar_position: 3
---

# Aggregate

## What is an Aggregate?

An aggregate is an entity.  
It requires an explicit identification field,  
And its state is expected to change during an instance’s lifecycle.

However, it is much more than just an entity.  
The aggregate is a **consistency enforcement boundary**.

## What Problem Aggregate Pattern is Trying to Solve?

Since an entity's data is mutable,  
It creates an opening for its data to become corrupted.

_The goal of the pattern is to protect the consistency of its data._

## What is Aggregate Pattern Solution?

The aggregate pattern draws a clear boundary between the aggregate and its outer scope.

The aggregate’s logic has to validate all incoming modifications,  
And ensure that the changes do not contradict its business rules.

## How to Implement Aggregate Pattern?

From an implementation perspective,  
The consistency is enforced by allowing only the aggregate’s business logic to modify its state.

All processes or objects external to the aggregate are only allowed to read the aggregate’s state.  
Its state can only be mutated by executing corresponding methods of the aggregate’s public interface.

The state-modifying methods,  
Are often referred to as _commands_, as in _a command to do something_.

An aggregate’s public interface is responsible for validating the input and enforcing all of the relevant business rules and invariants.

This strict boundary also ensures that all business logic related to the aggregate is implemented in one place:  
The aggregate itself.

### How to Implement a Command?

A command can be implemented in two ways:

1. It it can be implemented as a plain public method of the aggregate object:

   ```cs
   public class Ticket
   {
       public void AddMessage(UserId from, string body)
       {
           var message = new Message(from, body);
           _messages.Append(message);
       }
   }
   ```

1. It can be represented as a _parameter object_,  
   That encapsulates all the input required for executing the command:

   ```cs
   public class Ticket
   {
       public void Execute(AddMessage cmd)
       {
           var message = new Message(cmd.from, cmd.body);
           _messages.Append(message);
       }
   }
   ```

How commands are expressed in an aggregate’s code is a matter of preference.  
I prefer the more explicit way of defining command structures and passing them polymorphically to the relevant Execute method.

## References

- Learning Domain-Driven Design - Vladik Khononov - O'Reilly
