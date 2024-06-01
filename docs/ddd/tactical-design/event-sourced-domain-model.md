---
sidebar_position: 5
---

# Event-Sourced Domain Model

The event-sourced domain model pattern is based on the same premise as the domain model pattern.

the business logic is complex and belongs to a core subdomain.

Moreover, it uses the same tactical patterns as the domain model:  
Value objects, aggregates, and domain events.

The difference between these implementation patterns lies in the way the aggregates’ state is persisted.  
The event-sourced domain model uses the event sourcing pattern to manage the aggregates’ states:  
Instead of persisting an aggregate’s state,  
The model generates domain events describing each change and uses them as the source of truth for the aggregate’s data.

## Event Sourcing

> Show me your flowchart and conceal your tables, and I shall continue to be mystified.  
> Show me your tables, and I won’t usually need your flowchart; it’ll be obvious.  
> — Fred Brooks

Let’s use Fred Brooks’s reasoning to define the event sourcing pattern and understand how it differs from traditional modeling and persisting of data.
