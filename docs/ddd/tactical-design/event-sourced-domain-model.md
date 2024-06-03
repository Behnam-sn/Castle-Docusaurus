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

_The difference between these implementation patterns lies in the way the aggregates state is persisted._

The event-sourced domain model uses the **Event Sourcing Pattern**, to manage the aggregates’ states:  
Instead of persisting an aggregate’s state,  
The model generates domain events describing each change,  
And uses them as the source of truth for the aggregate’s data.

<!-- maybe the difference -->

## How to Implement Event-Sourced Domain Model Pattern?

## When to Use Event-Sourced Domain Model Pattern?
