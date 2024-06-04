---
sidebar_position: 6
---

# Event-Sourced Domain Model

## What is Event-Sourced Domain Model Pattern?

The event-sourced domain model pattern,  
Is based on the same premise as the domain model pattern:

- The business logic is complex and belongs to a core subdomain.
- And it uses the same tactical patterns as the domain model:  
  Value Objects, Aggregates, and Domain Events.

<!-- maybe the difference -->

_The difference between these implementation patterns lies in the way the aggregates state is persisted._

The event-sourced domain model uses the **Event Sourcing Pattern**,  
To manage the aggregates’ states:

Instead of persisting an aggregate’s state,  
The model generates domain events describing each change,  
And uses them as the source of truth for the aggregate’s data.

### Why Use The Term _Event-Sourced Domain Model_ Rather Than Just _Event Sourcing_?

Using events to represent state transitions (the event sourcing pattern),  
Is possible with or without the domain model’s building blocks.

Therefore, it's preferred to use the longer term,  
To explicitly state that we are using event sourcing,  
To represent changes in the lifecycles of the domain model’s aggregates.

## How to Implement Event-Sourced Domain Model Pattern?

The original domain model maintains a state representation of its aggregates and emits select domain events.  
The event-sourced domain model uses domain events exclusively for modeling the aggregates’ lifecycles.

All changes to an aggregate’s state have to be expressed as domain events.

Each operation on an event-sourced aggregate follows this script:

- Load the aggregate’s domain events.

- Reconstitute a state representation,  
  By projecting the events into a state representation that can be used to make business decisions.

- Execute the aggregate’s command to execute the business logic,  
  And consequently, produce new domain events.

- Commit the new domain events to the event store.

### Example

Going back to the example of the `Ticket` aggregate,  
Let’s see how it would be implemented as an event-sourced aggregate.

The application service follows the script described earlier:

- It loads the relevant ticket’s events,
- Rehydrates the aggregate instance,
- Calls the relevant command,
- And persists changes back to the database

```cs
public class TicketAPI
{
    private ITicketsRepository _ticketsRepository;

    public void RequestEscalation(TicketId id, EscalationReason reason)
    {
        var events = _ticketsRepository.LoadEvents(id);
        var ticket = new Ticket(events);
        var originalVersion = ticket.Version;
        var cmd = new RequestEscalation(reason);
        ticket.Execute(cmd);
        _ticketsRepository.CommitChanges(ticket, originalVersion);
    }
}
```

The `Ticket` aggregate’s rehydration logic in the constructor,  
Instantiates an instance of the state projector class `TicketState`,  
And sequentially calls its `AppendEvent` method for each of the ticket’s events:

```cs
public class Ticket
{
    private List<DomainEvent> _domainEvents = new List<DomainEvent>();
    private TicketState _state;

    public Ticket(IEnumerable<IDomainEvents> events)
    {
        _state = new TicketState();
        foreach (var e in events)
        {
            AppendEvent(e);
        }
    }

    private void AppendEvent(IDomainEvent @event)
    {
        _domainEvents.Append(@event);
        // Dynamically call the correct overload of the “Apply” method.
        ((dynamic)state).Apply((dynamic)@event);
    }

    public void Execute(RequestEscalation cmd)
    {
        if (!_state.IsEscalated && _state.RemainingTimePercentage <= 0)
        {
            var escalatedEvent = new TicketEscalated(_id, cmd.Reason);
            AppendEvent(escalatedEvent);
        }
    }
}
```

The `AppendEvent` passes the incoming events to the `TicketState` projection logic,  
Thus generating the in-memory representation of the ticket’s current state:

Contrary to the implementation we saw in the previously,  
The event-sourced aggregate’s `RequestEscalation` method,  
Doesn’t explicitly set the `IsEscalated` flag to `true`.  
Instead, it instantiates the appropriate event and passes it to the `AppendEvent` method.

All events added to the aggregate’s events collection,  
Are passed to the state projection logic in the `TicketState` class,  
Where the relevant fields’ values are mutated according to the events’ data:

```cs
public class TicketState
{
    public TicketId Id { get; private set; }
    public int Version { get; private set; }
    public bool IsEscalated { get; private set; }

    public void Apply(TicketInitialized @event)
    {
        Id = @event.Id;
        Version = 0;
        IsEscalated = false;
    }

    public void Apply(TicketEscalated @event)
    {
        IsEscalated = true;
        Version += 1;
    }
}
```

## What Are The Advantages of Event-Sourced Domain Model Pattern?

Compared to the more traditional model,  
In which the aggregates’ current states are persisted in a database,  
The event-sourced domain model requires more effort to model the aggregates.

However, this approach brings significant advantages that make the pattern worth considering in many scenarios:

- ### Time Traveling

  Just as the domain events can be used to reconstitute an aggregate’s current state,  
  They can also be used to restore all past states of the aggregate.

  In other words, you can always reconstitute all the past states of an aggregate.

  This is often done when analyzing the system’s behavior,  
  Inspecting the system’s decisions,  
  And optimizing the business logic.

  Another common use case for reconstituting past states is retroactive debugging:  
  You can revert the aggregate to the exact state it was in when a bug was observed.

- ### Deep Insight

  We know that optimizing core subdomains is strategically important for the business.

  Event sourcing provides deep insight into the system’s state and behavior.

  Event sourcing provides the flexible model,  
  That allows for transforming the events into different state representations.

  You can always add new projections that will leverage the existing events’ data to provide additional insights.

- ### Audit Log

  The persisted domain events,  
  Represent a strongly consistent audit log of everything that has happened to the aggregates states.

  Laws oblige some business domains to implement such audit logs,  
  And event sourcing provides this out of the box.

  This model is especially convenient for systems managing money or monetary transactions.  
  It allows us to easily trace the system’s decisions and the flow of funds between accounts.

- ### Advanced Optimistic Concurrency Management

  The classic optimistic concurrency model raises an exception,  
  When the read data becomes stale (overwritten by another process) while it is being written.

  When using event sourcing,  
  We can gain deeper insight into exactly what has happened between reading the existing events and writing the new ones.

  You can query the exact events that were concurrently appended to the event store,  
  And make a business domain–driven decision.

  As to whether the new events collide with the attempted operation,  
  Or the additional events are irrelevant and it’s safe to proceed.

## What Are The Disadvantages of Event-Sourced Domain Model Pattern?

So far it may seem that the event-sourced domain model is the ultimate pattern for implementing business logic,  
And thus should be used as often as possible.

Of course,  
That would contradict the principle of letting the business domain’s needs drive the design decisions.

So, let’s discuss some of the challenges presented by the pattern:

- ### Learning Curve

  The obvious disadvantage of the pattern is its sharp difference from the traditional techniques of managing data.  
  Successful implementation of the pattern demands training of the team and time to get used to the new way of thinking.

  Unless the team already has experience implementing event-sourced systems,  
  The learning curve has to be taken into account.

- ### Evolving the Model

  Evolving an event-sourced model can be challenging.  
  The strict definition of event sourcing says that events are immutable.

  But what if you need to adjust the event’s schema?  
  The process is not as simple as changing a table’s schema.

  In fact, a whole book was written on this subject alone:  
  Versioning in an Event Sourced System by Greg Young

- ### Architectural Complexity

  Implementation of event sources introduces numerous architectural “moving parts”,  
  Making the overall design more complicated.

All of these challenges are even more acute,  
If the task at hand doesn’t justify the use of the pattern.  
And instead can be addressed by a simpler design.

## Frequently Asked Questions

When engineers are introduced to the event sourcing pattern,  
They often ask several common questions.

- ### Performance

  Reconstituting an aggregate’s state from events will negatively affect the system’s performance.  
  It will degrade as events are added.

  How can this even work?

  Projecting events into a state representation indeed requires compute power,  
  And that need will grow as more events are added to an aggregate’s list.

  It’s important to benchmark a projection’s impact on performance:  
  The effect of working with hundreds or thousands of events.

  The results should be compared with the expected lifespan of an aggregate,  
  Which is the number of events expected to be recorded during an average lifespan.

  In most systems,  
  The performance hit will be noticeable only after 10,000+ events per aggregate.

  That said, in the vast majority of systems,  
  An aggregate’s average lifespan won’t go over 100 events.

  In the rare cases when projecting states does become a performance issue,  
  Another pattern can be implemented: snapshot.

<!-- page 113 -->

- ### Scalability

  This model generates enormous amounts of data.

  Can it scale?

  The event-sourced model is easy to scale.  
  Since all aggregate-related operations are done in the context of a single aggregate,  
  The event store can be sharded by aggregate IDs:  
  All events belonging to an instance of an aggregate should reside in a single shard.

- ### Deleting Data

  The event store is an append-only database,  
  But what if I do need to delete data physically;  
  For example, to comply with GDPR?

  This need can be addressed with the forgettable payload pattern: all sensitive
  information is included in the events in encrypted form. The encryption key is
  stored in an external key–value store: the key storage, where the key is a specific
  aggregate’s ID and the value is the encryption key. When the sensitive data has to
  be deleted, the encryption key is deleted from the key storage. As a result, the
  sensitive information contained in the events is no longer accessible.

- ### Why Can’t I Just…?

Why can’t I just write logs to a text file and use it as an audit log?
Writing data both to an operational database and to a logfile is an error-prone
operation. In its essence, it’s a transaction against two storage mechanisms: the
database and the file. If the first one fails, the second one has to be rolled back.
For example, if a database transaction fails, no one cares to delete the prior log
messages. Hence, such logs are not consistent, but rather, eventually inconsistent.

Why can’t I keep working with a state-based model, but in the same database transac‐
tion, append logs to a logs table?
From an infrastructural perspective, this approach does provide consistent syn‐
chronization between the state and the log records. However, it is still error
prone. What if the engineer who will be working on the codebase in the future
forgets to append an appropriate log record?

Furthermore, when the state-based representation is used as the source of truth,
the additional log table’s schema usually degrades into chaos quickly. There is no
way to enforce that all required information is written and that it is written in the
correct format.

Why can’t I just keep working with a state-based model but add a database trigger that
will take a snapshot of the record and copy it into a dedicated “history” table?
This approach overcomes the previous one’s drawback: no explicit manual calls
are needed to append records to the log table. That said, the resultant history
only includes the dry facts: what fields were changed. It misses the business con‐
texts: why the fields were changed. The lack of “why” drastically limits the ability
to project additional models.
