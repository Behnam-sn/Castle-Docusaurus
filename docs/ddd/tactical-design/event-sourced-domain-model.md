---
sidebar_position: 5
---

# Event-Sourced Domain Model

The event-sourced domain model pattern is based on the same premise as the domain model pattern.  
The business logic is complex and belongs to a core subdomain.

Moreover, it uses the same tactical patterns as the domain model:  
Value Objects, Aggregates, and Domain Events.

The difference between these implementation patterns lies in the way the aggregates’ state is persisted.

The event-sourced domain model uses the **event sourcing pattern** to manage the aggregates’ states:  
Instead of persisting an aggregate’s state,  
The model generates domain events describing each change and uses them as the source of truth for the aggregate’s data.

## Why “Event-Sourced Domain Model”?

I feel obliged to explain why I use the term _event-sourced domain model_ rather than just _event sourcing_.

Using events to represent state transitions (the event sourcing pattern),  
Is possible with or without the domain model’s building blocks.

Therefore, I prefer the longer term to explicitly state that we are using event sourcing to represent changes in the lifecycles of the domain model’s aggregates.

## Event Sourcing

> Show me your flowchart and conceal your tables, and I shall continue to be mystified.  
> Show me your tables, and I won’t usually need your flowchart; it’ll be obvious.  
> — Fred Brooks

Let’s use Fred Brooks’s reasoning to define the event sourcing pattern,  
And understand how it differs from traditional modeling and persisting of data.

It’s evident that the table is used to manage potential customers, or leads, in a telemarketing system.

For each lead, you can see:

- their ID
- Their first and last names
- When the record was created and updated
- Their phone number
- And the lead’s current status

By examining the various statuses,  
We can also assume the processing cycle each potential customer goes through:

- The sales flow starts with the potential customer in the `NEW_LEAD` status.
- A sales call can end with:  
  The person not being interested in the offer (the lead is `CLOSED`),  
  Scheduling a follow-up call (`FOLLOWUP_SET`),  
  Or accepting the offer (`PENDING_PAYMENT`).
- If the payment is successful, the lead is `CONVERTED` into a customer.  
  Conversely, the payment can fail (`PAYMENT_FAILED`).

That’s quite a lot of information that we can gather just by analyzing a table’s schema and the data stored in it.

<!-- We can even assume what ubiquitous language was used when modeling the data. -->

But what information is missing from that table?

The table’s data documents the leads’ current states,  
But it misses the story of how each lead got to their current state.

We can’t analyze what was happening during the lifecycles of leads:

- We don’t know how many calls were made before a lead became `CONVERTED`.
- Was a purchase made right away, or was there a lengthy sales journey?
- Based on the historical data,  
  Is it worth trying to contact a person after multiple follow-ups,  
  Or is it more efficient to close the lead and move to a more promising prospect?

None of that information is there.  
All we know are the leads’ current states.

These questions reflect business concerns essential for optimizing the sales process.  
From a business standpoint,  
It’s crucial to analyze the data and optimize the process based on the experience.

One of the ways to fill in the missing information is to use **Event Sourcing**.

_The event sourcing pattern introduces the dimension of time into the data model._

Instead of the schema reflecting the aggregates’ current state,  
An event sourcing based system persists events documenting every change in an aggregate’s lifecycle.

Consider the `CONVERTED` customer on line 12 in Table 7-1.  
The following listing demonstrates how the person’s data would be represented in an event-sourced system:

```json
{
    "lead-id": 12,
    "event-id": 0,
    "event-type": "lead-initialized",
    "first-name": "Casey",
    "last-name": "David",
    "phone-number": "555-2951",
    "timestamp": "2020-05-20T09:52:55.95Z"
},
{
    "lead-id": 12,
    "event-id": 1,
    "event-type": "contacted",
    "timestamp": "2020-05-20T12:32:08.24Z"
},
{
    "lead-id": 12,
    "event-id": 2,
    "event-type": "followup-set",
    "followup-on": "2020-05-27T12:00:00.00Z",
    "timestamp": "2020-05-20T12:32:08.24Z"
},
{
    "lead-id": 12,
    "event-id": 3,
    "event-type": "contact-details-updated",
    "first-name": "Casey",
    "last-name": "Davis",
    "phone-number": "555-8101",
    "timestamp": "2020-05-20T12:32:08.24Z"
},
{
    "lead-id": 12,
    "event-id": 4,
    "event-type": "contacted",
    "timestamp": "2020-05-27T12:02:12.51Z"
},
{
    "lead-id": 12,
    "event-id": 5,
    "event-type": "order-submitted",
    "payment-deadline": "2020-05-30T12:02:12.51Z",
    "timestamp": "2020-05-27T12:02:12.51Z"
},
{
    "lead-id": 12,
    "event-id": 6,
    "event-type": "payment-confirmed",
    "status": "converted",
    "timestamp": "2020-05-27T12:38:44.12Z"
}
```

The events in the listing tell the customer’s story:

- The lead was created in the system (event 0)
- And was contacted by a sales agent about two hours later (event 1)
- During the call, it was agreed that the sales agent would call back a week later (event 2)
- But to a different phone number (event 3).  
  The sales agent also fixed a typo in the last name (event 3).
- The lead was contacted on the agreed date and time (event 4)
- And submitted an order (event 5).  
  The order was to be paid in three days (event 5),
- but the payment was received about half an hour later (event 6),  
  And the lead was converted into a new customer.

As we can see,  
The customer’s state can easily be projected out from these domain events.

All we have to do is apply simple transformation logic sequentially to each event:

```cs
public class LeadModelProjection
{
    public long LeadId { get; private set; }
    public string FirstName { get; private set; }
    public string LastName { get; private set; }
    public LeadStatus Status { get; private set; }
    public PhoneNumber PhoneNumber { get; private set; }
    public DateTime FollowupOn { get; private set; }
    public DateTime CreatedOn { get; private set; }
    public DateTime UpdatedOn { get; private set; }
    public int Version { get; private set; }

    public void Apply(LeadInitialized @event)
    {
        LeadId = @event.LeadId;
        FirstName = @event.FirstName;
        LastName = @event.LastName;
        PhoneNumber = @event.PhoneNumber;
        Version = 0;
    }

    public void Apply(ContactDetailsChanged @event)
    {
        FirstName = @event.FirstName;
        LastName = @event.LastName;
        PhoneNumber = @event.PhoneNumber;
        Version += 1;
    }

    public void Apply(Contacted @event)
    {
        Version += 1;
    }

    public void Apply(FollowupSet @event)
    {
        Version += 1;
    }

    public void Apply(OrderSubmitted @event)
    {
        Version += 1;
    }

    public void Apply(PaymentConfirmed @event)
    {
        Version += 1;
    }
}
```

Iterating an aggregate’s events,  
And feeding them sequentially,  
Into the appropriate overrides of the Apply method,  
Will produce precisely the state representation modeled in the table.

Pay attention to the `Version` field that is incremented after applying each event.  
Its value represents the total number of modifications made to the business entity.

Suppose we apply a subset of events;  
In that case, we can “travel through time”:  
We can project the entity’s state at any point of its lifecycle by applying only the relevant events.

For example,  
If we need the entity’s state in version 5,  
We can apply only the first five events.

Finally,  
We are not limited to projecting only a single state representation of the events!  
Consider the following scenarios.

### Search

If you have to implement a search.

Since a lead’s contact information including first name, last name, and phone number can be updated;  
Sales agents may not be aware of the changes applied by other agents,  
And may want to locate leads using their contact information, including historical values.

We can easily project the historical information:

```cs
public class LeadSearchModelProjection
{
    public long LeadId { get; private set; }
    public HashSet<string> FirstNames { get; private set; }
    public HashSet<string> LastNames { get; private set; }
    public HashSet<PhoneNumber> PhoneNumbers { get; private set; }
    public int Version { get; private set; }

    public void Apply(LeadInitialized @event)
    {
        FirstNames = new HashSet<string>();
        LastNames = new HashSet<string>();
        PhoneNumbers = new HashSet<PhoneNumber>();

        LeadId = @event.LeadId;
        FirstNames.Add(@event.FirstName);
        LastNames.Add(@event.LastName);
        PhoneNumbers.Add(@event.PhoneNumber);
        Version = 0;
    }

    public void Apply(ContactDetailsChanged @event)
    {
        FirstNames.Add(@event.FirstName);
        LastNames.Add(@event.LastName);
        PhoneNumbers.Add(@event.PhoneNumber);
        Version += 1;
    }

    public void Apply(Contacted @event)
    {
        Version += 1;
    }

    public void Apply(FollowupSet @event)
    {
        Version += 1;
    }

    public void Apply(OrderSubmitted @event)
    {
        Version += 1;
    }

    public void Apply(PaymentConfirmed @event)
    {
        Version += 1;
    }
}
```

The projection logic uses the `LeadInitialized` and `ContactDetailsChanged` events,  
To populate the respective sets of the lead’s personal details.

Other events are ignored since they do not affect the specific model’s state.

Applying this projection logic to Casey Davis’s events from the earlier example will result in the following state:

```txt
LeadId: 12
FirstNames: ['Casey']
LastNames: ['David', 'Davis']
PhoneNumbers: ['555-2951', '555-8101']
Version: 6
```

### Analysis

Your business intelligence department asks you to provide a more analysis-friendly representation of the leads data.  
For their current research, they want to get the number of follow-up calls scheduled for different leads.  
Later they will filter the converted and closed leads data and use the model to optimize the sales process.  
Let’s project the data they are asking for:

```cs
public class AnalysisModelProjection
{
    public long LeadId { get; private set; }
    public int Followups { get; private set; }
    public LeadStatus Status { get; private set; }
    public int Version { get; private set; }

    public void Apply(LeadInitialized @event)
    {
        LeadId = @event.LeadId;
        Followups = 0;
        Status = LeadStatus.NEW_LEAD;
        Version = 0;
    }

    public void Apply(Contacted @event)
    {
        Version += 1;
    }

    public void Apply(FollowupSet @event)
    {
        Status = LeadStatus.FOLLOWUP_SET;
        Followups += 1;
        Version += 1;
    }

    public void Apply(ContactDetailsChanged @event)
    {
        Version += 1;
    }

    public void Apply(OrderSubmitted @event)
    {
        Status = LeadStatus.PENDING_PAYMENT;
        Version += 1;
    }

    public void Apply(PaymentConfirmed @event)
    {
        Status = LeadStatus.CONVERTED;
        Version += 1;
    }
}
```

The preceding logic maintains a counter of the number of times follow-up events appeared in the lead’s events.  
If we were to apply this projection to the example of the aggregate’s events, it would generate the following state:

```txt
LeadId: 12
Followups: 1
Status: Converted
Version: 6
```

The logic implemented in the preceding examples projects the search-optimized and analysis-optimized models in-memory.  
However, to actually implement the required functionality, we have to persist the projected models in a database.

You will learn about a pattern that allows us to do that:  
command-query responsibility segregation (CQRS).

## Source of Truth

For the event sourcing pattern to work,  
All changes to an object’s state should be represented and persisted as events.

These events become the system’s source of truth (hence the name of the pattern).

The database that stores the system’s events is the only strongly consistent storage:  
The system’s source of truth.

The accepted name for the database that is used for persisting events is **Event Store**.

## Event Store

The event store is a append-only storage.  
And should not allow modifying or deleting the events.  
Except for exceptional cases, such as data migration.

To support implementation of the event sourcing pattern,  
At a minimum the event store has to support the following functionality:

- Fetch all events belonging to a specific business entity
- And append the events

For example:

```cs
interface IEventStore
{
    IEnumerable<Event> Fetch(Guid instanceId);
    void Append(Guid instanceId, Event[] newEvents, int expectedVersion);
}
```

The `expectedVersion` argument in the `Append` method is needed to implement optimistic concurrency management:

When you append new events,  
You also specify the version of the entity on which you are basing your decisions.

If it’s stale, that is, new events were added after the expected version,  
The event store should raise a concurrency exception.

In most systems, additional endpoints are needed for implementing the CQRS pattern.

:::note
In essence, the event sourcing pattern is nothing new.  
The financial industry uses events to represent changes in a ledger.  
A ledger is an append-only log that documents transactions.  
A current state (e.g., account balance) can always be deduced by “projecting” the ledger’s records.
:::

## Event-Sourced Domain Model Pattern

The original domain model maintains a state representation of its aggregates and emits select domain events.  
The event-sourced domain model uses domain events exclusively for modeling the aggregates’ lifecycles.

All changes to an aggregate’s state have to be expressed as domain events.

Each operation on an event-sourced aggregate follows this script:

- Load the aggregate’s domain events.
- Reconstitute a state representation—project the events into a state representation that can be used to make business decisions.
- Execute the aggregate’s command to execute the business logic, and consequently, produce new domain events.
- Commit the new domain events to the event store.

Going back to the example of the `Ticket` aggregate,  
Let’s see how it would be implemented as an event-sourced aggregate.

The application service follows the script described earlier:  
It loads the relevant ticket’s events,  
Rehydrates the aggregate instance,  
Calls the relevant command,  
And persists changes back to the database:

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
Instantiates an instance of the state projector class, `TicketState`,  
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
The event-sourced aggregate’s RequestEscalation method doesn’t explicitly set the `IsEscalated` flag to `true`.  
Instead, it instantiates the appropriate event and passes it to the `AppendEvent` method.

All events added to the aggregate’s events collection are passed to the state projection logic in the `TicketState` class,  
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

Now let’s look at some of the advantages of leveraging event sourcing when implementing complex business logic.

### Advantages

Compared to the more traditional model,  
In which the aggregates’ current states are persisted in a database,  
The event-sourced domain model requires more effort to model the aggregates.

However, this approach brings significant advantages that make the pattern worth considering in many scenarios:

- #### Time traveling

  Just as the domain events can be used to reconstitute an aggregate’s current state,  
  they can also be used to restore all past states of the aggregate.  
  In other words, you can always reconstitute all the past states of an aggregate.

  This is often done when analyzing the system’s behavior,  
  Inspecting the system’s decisions,  
  And optimizing the business logic.

  Another common use case for reconstituting past states is retroactive debugging:  
  You can revert the aggregate to the exact state it was in when a bug was observed.

- #### Deep insight

  We know that optimizing core subdomains is strategically important for the business.  
  Event sourcing provides deep insight into the system’s state and behavior.

  As you learned earlier in this chapter,  
  Event sourcing provides the flexible model that allows for transforming the events into different state representations,
  You can always add new projections that will leverage the existing events’ data to provide additional insights.

- #### Audit log

  The persisted domain events represent a strongly consistent audit log of everything that has happened to the aggregates’ states.

  Laws oblige some business domains to implement such audit logs,  
  And event sourcing provides this out of the box.

  This model is especially convenient for systems managing money or monetary transactions.  
  It allows us to easily trace the system’s decisions and the flow of funds between accounts.

- #### Advanced optimistic concurrency management

  The classic optimistic concurrency model raises an exception,  
  When the read data becomes stale (overwritten by another process) while it is being written.

  When using event sourcing,  
  We can gain deeper insight into exactly what has happened between reading the existing events and writing the new ones.  
  You can query the exact events that were concurrently appended to the event store,  
  And make a business domain–driven decision,  
  As to whether the new events collide with the attempted operation,  
  Or the additional events are irrelevant and it’s safe to proceed.

### Disadvantages

So far it may seem that the event-sourced domain model is the ultimate pattern for implementing business logic,  
And thus should be used as often as possible.

Of course,
That would contradict the principle of letting the business domain’s needs drive the design decisions.

So, let’s discuss some of the challenges presented by the pattern:

- #### Learning curve

  The obvious disadvantage of the pattern is its sharp difference from the traditional techniques of managing data.  
  Successful implementation of the pattern demands training of the team and time to get used to the new way of thinking.

  Unless the team already has experience implementing event-sourced systems,  
  The learning curve has to be taken into account.

- #### Evolving the model

  Evolving an event-sourced model can be challenging.  
  The strict definition of event sourcing says that events are immutable.

  But what if you need to adjust the event’s schema?  
  The process is not as simple as changing a table’s schema.

  In fact, a whole book was written on this subject alone:  
  Versioning in an Event Sourced System by Greg Young.

- #### Architectural complexity

  Implementation of event sources introduces numerous architectural “moving parts”,  
  Making the overall design more complicated.

All of these challenges are even more acute,  
If the task at hand doesn’t justify the use of the pattern and instead can be addressed by a simpler design.

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

- ### This model generates enormous amounts of data. Can it scale?

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
