---
sidebar_position: 4
---

# Domain Events

## What is a Domain Event?

A domain event is a message describing a significant event that has occurred in the business domain.

For example:

- Ticket assigned
- Ticket escalated
- Message received

:::tip
Since domain events describe something that has already happened,  
Their names should be formulated in the past tense.
:::

## What Problem Domain Events are Trying to Solve?

The goal of a domain event is to describe what has happened in the business domain,  
And provide all the necessary data related to the event.

For example:  
The following domain event communicates,  
That the specific ticket was escalated, at what time, and for what reason:

```json
{
  "ticket-id": "c9d286ff-3bca-4f57-94d4-4d4e490867d1",
  "event-id": 146,
  "event-type": "ticket-escalated",
  "escalation-reason": "missed-sla",
  "escalation-time": 1628970815
}
```

:::tip
As with almost everything in software engineering, naming is important.  
Make sure the names of the domain events succinctly reflect exactly what has happened in the business domain.
:::

## How to Implement Domain Events?

Domain events are part of an aggregate’s public interface.

An aggregate publishes its domain events.  
Other processes, aggregates, or even external systems,  
Can subscribe to and execute their own logic in response to the domain events.

In the following excerpt from the `Ticket` aggregate,  
A new domain event is instantiated,  
And appended to the collection of the ticket’s domain events:

```cs
public class Ticket
{
    private List<DomainEvent> _domainEvents;

    public void Execute(RequestEscalation cmd)
    {
        if (!this.IsEscalated && this.RemainingTimePercentage <= 0)
        {
            this.IsEscalated = true;
            var escalatedEvent = new TicketEscalated(_id, cmd.Reason);
            _domainEvents.Append(escalatedEvent);
        }
    }
}
```

In Chapter 9, we will discuss how domain events can be reliably published to interested subscribers.

## References

- Learning Domain-Driven Design - Vladik Khononov - O'Reilly
