---
sidebar_position: 3
---

# Aggregates

## What is an Aggregate?

An aggregate is an entity.  
It requires an explicit identification field and its state is expected to change during an instance’s lifecycle.

However, it is much more than just an entity.

<!-- ## Why of Aggregate -->

Since an aggregate’s data is mutable,  
It creates an opening for multiple ways in which its data can become corrupted.

The goal of the pattern is to protect the consistency of its data.  
There are implications and challenges that the pattern has to address to keep its state consistent at all times.

<!-- ### Consistency Enforcement -->

## How Aggregate Enforces Consistency?

To enforce consistency of the data,  
The aggregate pattern draws a clear boundary between the aggregate and its outer scope.

_The aggregate is a consistency enforcement boundary._

The aggregate’s logic has to validate all incoming modifications and ensure that the changes do not contradict its business rules.

From an implementation perspective,  
The consistency is enforced by allowing only the aggregate’s business logic to modify its state.

All processes or objects external to the aggregate are only allowed to read the aggregate’s state.  
Its state can only be mutated by executing corresponding methods of the aggregate’s public interface.

The state-modifying methods exposed as an aggregate’s public interface are often referred to as _commands_, as in “a command to do something”.

An aggregate’s public interface is responsible for validating the input and enforcing all of the relevant business rules and invariants.

This strict boundary also ensures that all business logic related to the aggregate is implemented in one place:  
The aggregate itself.

### How to Implement a command?

A command can be implemented in two ways:

It it can be implemented as a plain public method of the aggregate object:

```cs
public class Ticket
{
    ...
    public void AddMessage(UserId from, string body)
    {
        var message = new Message(from, body);
        _messages.Append(message);
    }
    ...
}
```

Alternatively, a command can be represented as a _parameter object_ that encapsulates all the input required for executing the command:

```cs
public class Ticket
{
...
public void Execute(AddMessage cmd)
{
var message = new Message(cmd.from, cmd.body);
_messages.Append(message);
}
...
}
```

How commands are expressed in an aggregate’s code is a matter of preference.  
I prefer the more explicit way of defining command structures and passing them polymorphically to the relevant Execute method.

## Aggregate & Databases

### Concurrency

It’s vital to protect the consistency of an aggregate’s state.

If multiple processes are concurrently updating the same aggregate,  
We have to prevent the latter transaction from blindly overwriting the changes committed by the first one.  
In such a case, the second process has to be notified that the state on which it had based its decisions is out of date, and it has to retry the operation.

Hence, the database used for storing aggregates has to support concurrency management.

In its simplest form, an aggregate should hold a version field that will be incremented after each update:

```cs
class Ticket
{
    TicketId _id;
    int _version;
    ...
}
```

When committing a change to the database,  
We have to ensure that the version that is being overwritten matches the one that was originally read.  
For example, in SQL:

```sql
UPDATE tickets
SET ticket_status = @new_status,
agg_version = agg_version + 1
WHERE ticket_id=@id and agg_version=@expected_version;
```

This SQL statement applies changes made to the aggregate instance’s state (line 2),  
And increases its version counter (line 3),  
but only if the current version equals the one that was read prior to applying changes to the aggregate’s state (line 4).

:::note
Of course, concurrency management can be implemented elsewhere besides a relational database.  
Furthermore, document databases lend themselves more toward working with aggregates.

**It’s crucial to ensure that the database used for storing an aggregate’s data supports concurrency management.**
:::

### Transaction Boundary

Since an aggregate’s state can only be modified by its own business logic,  
the aggregate also acts as a transactional boundary.

All changes to the aggregate’s state should be committed transactionally as one atomic operation.  
If an aggregate’s state is modified, either all the changes are committed or none of them is.

Furthermore, no system operation can assume a multi-aggregate transaction.  
A change to an aggregate’s state can only be committed individually, one aggregate per database transaction.

The one aggregate instance per transaction forces us to carefully design an aggregate’s boundaries, ensuring that the design addresses the business domain’s invariants and rules.  
The need to commit changes in multiple aggregates signals a wrong transaction boundary, and hence, wrong aggregate boundaries.

This seems to impose a modeling limitation.  
What if we need to modify multiple objects in the same transaction?  
Let’s see how the pattern addresses such situations.

## Aggregate vs Entity

### Hierarchy of entities

As we discussed earlier, we don’t use entities as an independent pattern, only as part of an aggregate.

Let’s see the fundamental difference between entities and aggregates, and why entities are a building block of an aggregate rather than of the overarching domain model.

There are business scenarios in which multiple objects should share a transactional boundary;  
For example, when both can be modified simultaneously,  
Or the business rules of one object depend on the state of another object.

DDD prescribes that a system’s design should be driven by its business domain.  
Aggregates are no exception.  
To support changes to multiple objects that have to be applied in one atomic transaction,  
the aggregate pattern resembles a hierarchy of entities, all sharing transactional consistency.

The hierarchy contains both entities and value objects,  
and all of them belong to the same aggregate if they are bound by the domain’s business logic.

That’s why the pattern is named “aggregate”:  
It aggregates business entities and value objects that belong to the same transaction boundary.

The aggregate ensures that all the conditions are checked against strongly consistent data,  
And it won’t change after the checks are completed by ensuring that all changes to the aggregate’s data are performed as one atomic transaction.