---
sidebar_position: 4
---

# Event Sourcing

## What is Event Sourcing?

_Event sourcing ensures that all changes to application state are stored as a sequence of events._

## What Problem is Event Sourcing Trying to Solve?

> Show me your flowchart and conceal your tables,  
> And I shall continue to be mystified.
>
> Show me your tables,  
> And I won’t usually need your flowchart;  
> It’ll be obvious.
>
> — Fred Brooks

Let’s use Fred Brooks’s reasoning to understand,  
How the event sourcing pattern differs from traditional modeling and persisting of data.

Take a look at this table for example:

| lead-id | first-name | last-name |     status      | phone-number |       followup-on        |        created-on        |        updated-on        |
| :-----: | :--------: | :-------: | :-------------: | :----------: | :----------------------: | :----------------------: | :----------------------: |
|    1    |   Sarah    |  Estrada  |     CLOSED      |   555-4395   |                          | 2019-03-29T 22:01:41.44Z | 2019-03-29T 22:01:41.44Z |
|    2    |  Samantha  |   Chan    |    NEW_LEAD     |   555-8861   |                          | 2019-07-17T 13:09:59.32Z | 2019-07-17T 13:09:59.32Z |
|    3    |    Sian    | Espinoza  |  FOLLOWUP_SET   |   555-6461   | 2019-12-04T 01:49:08.05Z | 2019-07-17T 13:09:59.32Z | 2019-12-04T 01:49:08.05Z |
|    4    |   Casey    |   Davis   |    CONVERTED    |   555-8101   |                          | 2020-05-20T 09:52:55.95Z | 2020-05-20T 09:52:55.95Z |
|    5    |    Sara    |  Elliott  | PENDING_PAYMENT |   555-2620   |                          | 2020-08-12T 17:39:43.25Z | 2020-08-12T 17:39:43.25Z |
|    6    |   Sally    |   Evans   | PAYMENT_FAILED  |   555-3230   |                          | 2020-06-04T 14:51:06.15Z | 2020-06-04T 14:51:06.15Z |

It’s evident that the table is used to manage potential customers, or leads, in a telemarketing system.

For each lead, you can see:

- Their ID
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

**But what information is missing from that table?**

The table’s data documents the leads’ current states,  
But it misses the story of how each lead got to their current state.

We can’t analyze what was happening during the lifecycles of leads:

- How many calls were made before a lead became `CONVERTED`?
- Was a purchase made right away?  
  Or was there a lengthy sales journey?
- Based on the historical data,  
  Is it worth trying to contact a person after multiple follow-ups?  
  Or is it more efficient to close the lead and move to a more promising prospect?

None of that information is there.  
All we know are the leads’ current states.  
These questions reflect business concerns essential for optimizing the sales process.  
From a business standpoint,  
It’s crucial to analyze the data and optimize the process based on the experience.

One of the ways to fill in the missing information is to use **Event Sourcing**.

## What is Event Souring Solution?

_The event sourcing pattern introduces the dimension of time into the data model._

Instead of the schema reflecting the aggregates’ current state,  
An event sourcing based system persists events documenting every change in an aggregate’s lifecycle.

Consider the `CONVERTED` customer on line 4 in Table.  
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

## How to Implement Event Souring?

### State Projection

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
    public int Version { get; private set; }

    public void Apply(LeadInitialized @event)
    {
        LeadId = @event.LeadId;
        FirstName = @event.FirstName;
        LastName = @event.LastName;
        Status = LeadStatus.NEW_LEAD;
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
        Status = LeadStatus.CONTACTED;
        Version += 1;
    }

    public void Apply(FollowupSet @event)
    {
        Status = LeadStatus.FOLLOWUP_SET;
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

Iterating an aggregate’s events,  
And feeding them sequentially,  
Into the appropriate overrides of the `Apply` method,  
Will produce precisely the state representation modeled in the table.

Pay attention to the `Version` field that is incremented after applying each event.  
It's value represents the total number of modifications made to the business entity.

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

Since a lead’s contact information including first name, last name, and phone number can be updated;  
Sales agents may not be aware of the changes applied by other agents,  
And may want to locate leads using their contact information,  
Including historical values.

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

For their current research,  
They want to get the number of follow-up calls scheduled for different leads.

Later they will filter the converted and closed leads data,  
And use the model to optimize the sales process.

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
If we were to apply this projection to the example of the aggregate’s events,  
It would generate the following state:

```txt
LeadId: 12
Followups: 1
Status: Converted
Version: 6
```

## How to Persist Events?

The logic implemented in the preceding examples,  
Projects the search-optimized and analysis-optimized models in-memory.

However,  
To actually implement the required functionality,  
We have to persist the projected models in a database.

### Source of Truth

For the event sourcing pattern to work,  
All changes to an object’s state should be represented and persisted as events.

These events become the system’s source of truth (hence the name of the pattern).

The database that stores the system’s events is the only strongly consistent storage:  
The system’s source of truth.

The accepted name for the database that is used for persisting events is **Event Store**.

### Event Store

The event store is a append-only storage.  
And should not allow modifying or deleting the events.

Except for exceptional cases,  
Such as data migration.

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

In most systems,  
Additional endpoints are needed for implementing the CQRS pattern.

You will learn about a pattern that allows us to do that:  
command-query responsibility segregation (CQRS).

:::note
In essence, the event sourcing pattern is nothing new.  
The financial industry uses events to represent changes in a ledger.  
A ledger is an append-only log that documents transactions.  
A current state (e.g., account balance) can always be deduced by “projecting” the ledger’s records.
:::

## Recap

Not just can we query these events,  
We can also use the event log to reconstruct past states,  
And as a foundation to automatically adjust the state to cope with retroactive changes.

Instead of storing just the current state of the data in a domain,  
You can use an append-only store to record the full series of actions taken on that data.

The store acts as the system of record,  
And can be used to materialize the domain objects.

This can simplify tasks in complex domains,  
By avoiding the need to synchronize the data model and the business domain,  
While improving performance, scalability, and responsiveness.

It can also provide consistency for transactional data,  
And maintain full audit trails and history that can enable compensating actions.

## References

- Learning Domain-Driven Design - Vladik Khononov - O'Reilly
- https://learn.microsoft.com/en-us/azure/architecture/patterns/event-sourcing
- https://www.martinfowler.com/eaaDev/EventSourcing.html
