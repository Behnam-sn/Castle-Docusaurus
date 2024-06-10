---
sidebar_position: 3
---

# Tactical Design Concerns

The main indicator of a change in a subdomain’s type is the inability of the existing technical design to support current business needs.

Let’s go back to the example of a supporting subdomain becoming a core subdomain.  
Supporting subdomains are implemented with relatively simple design patterns for modeling the business logic:  
Namely, the transaction script or active record pattern.  
As you know these patterns are not a good fit for business logic involving complex rules and invariants.

If complicated rules and invariants are added to the business logic over time,  
The codebase will become increasingly complex as well.

It will be painful to add the new functionality,  
As the design won’t support the new level of complexity.

This “pain” is an important signal.  
Use it as a call to reassess the business domain and design choices.

The need for change in the implementation strategy is nothing to fear.  
It’s normal.  
We cannot foresee how a business will evolve down the road.

We also cannot apply the most elaborate design patterns for all types of subdomains;  
That would be wasteful and ineffective.

We have to choose the most appropriate design and evolve it when needed.

If the decision for how to model the business logic is made consciously,  
And you are aware of all the possible design choices and the differences between them,  
Migrating from one design pattern to another is not that troublesome.

The following subsections highlight a few examples.

## Transaction Script to Active Record

At their core,  
Both the transaction script and active record patterns are based on the same principle:  
The business logic is implemented as a procedural script.

The difference between them is how the data structures are modeled:  
The active record pattern introduces the data structures to encapsulate the complexity of mapping them to the storage mechanism.

As a result,  
When working with data becomes challenging in a transaction script,  
Refactor it into the active record pattern.

Look for complicated data structures and encapsulate them in active record objects.  
Instead of accessing the database directly,  
Use active records to abstract its model and structure.

## Active Record to Domain Model

If the business logic that manipulates active records becomes complex,  
And you notice more and more cases of inconsistencies and duplications,  
Refactor the implementation to the domain model pattern.

Start by identifying value objects.  
What data structures can be modeled as immutable objects?  
Look for the related business logic,  
And make it a part of the value objects as well.

Next, analyze the data structures and look for transactional boundaries.  
To ensure that all state-modifying logic is explicit,  
Make all of the active records’ setters private,  
So that they can only be modified from inside the active record itself.

Obviously,
Expect the compilation to fail;  
However, the compilation errors will make it clear where the state-modifying logic resides.  
Refactor it into the active record’s boundaries.

For example:

```cs
public class Player
{
    public Guid Id { get; set; }
    public int Points { get; set; }
}

public class ApplyBonus
{
    public void Execute(Guid playerId, byte percentage)
    {
        var player = _repository.Load(playerId);
        player.Points *= 1 + percentage / 100.0;
        _repository.Save(player);
    }
}
```

In the following code,  
You can see the first steps toward the transformation.

The code won’t compile yet,  
But the errors will make it explicit where external components are controlling the object’s state:

```cs
public class Player
{
    public Guid Id { get; private set; }
    public int Points { get; private set; }
}

public class ApplyBonus
{
    public void Execute(Guid playerId, byte percentage)
    {
        var player = _repository.Load(playerId);
        player.Points *= 1 + percentage / 100.0;
        _repository.Save(player);
    }
}
```

In the next iteration,  
We can move that logic inside the active record’s boundary:

```cs
public class Player
{
    public Guid Id { get; private set; }
    public int Points { get; private set; }

    public void ApplyBonus(int percentage)
    {
        this.Points *= 1 + percentage / 100.0;
    }
}

public class ApplyBonus
{
    public void Execute(Guid playerId, int percentage)
    {
        var player = _repository.Load(playerId);
        player.ApplyBonus(percentage);
        _repository.Save(player);
    }
}
```

When all the state-modifying business logic is moved inside the boundaries of the corresponding objects,  
Examine what hierarchies are needed to ensure strongly consistent checking of business rules and invariants.

Those are good candidates for aggregates.

Keeping in mind the aggregate design principles we discussed,  
Look for the smallest transaction boundaries,  
That is, the smallest amount of data that you need to keep strongly consistent.

Decompose the hierarchies along those boundaries.  
Make sure the external aggregates are only referenced by their IDs.

Finally, for each aggregate,  
Identify its root, or the entry point for its public interface.

Make the methods of all the other internal objects in the aggregate private,  
And only callable from within the aggregate.

## Domain Model to Event-Sourced Domain Model

Once you have a domain model with properly designed aggregate boundaries,  
You can transition it to the event-sourced model.

Instead of modifying the aggregate’s data directly,  
Model the domain events needed to represent the aggregate’s lifecycle.

The most challenging aspect of refactoring a domain model into an event-sourced domain model is the history of the existing aggregates:  
Migrating the “timeless” state into the event-based model.

Since the fine-grained data representing all the past state changes is not there,  
You have to either generate past events on a best-effort basis or model migration events.

### Generating Past Transitions

This approach entails generating an approximate stream of events for each aggregate so that the stream of events can be projected into the same state representation as in the original implementation.

For example:

page 176

### Modeling Migration Events
