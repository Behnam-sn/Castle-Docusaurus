---
sidebar_position: 99
---

# Extras

## Business Problems

In that case, they won’t be able to completely understand the business logic or why it operates the way it does, which will limit their ability to model and implement an effective solution.

Again, DDD provides guidance and patterns for organizing these domains and avoiding further complexity.  
Tactical design continues the partnership with the domain experts who will recognize their domain language even as they look at the code built by the software teams.

Domain-driven design’s tactical tools address a different aspect of communication issues.

## application layer

In essence, the application layer’s operations implement the transaction script pattern. It has to orchestrate the
operation as an atomic transaction. The changes to the whole aggregate either succeed or fail, but never com‐
mit a partially updated state.

### Aggregate & Application layer

Aggregates makes the application layer that orchestrates operations on aggregates rather simple.  
All it has to do is load the aggregate’s current state,  
execute the required action,  
persist the modified state,  
and return the operation’s result to the caller:

```cs
public ExecutionResult Escalate(TicketId id, EscalationReason reason)
{
    try
    {
        var ticket = _ticketRepository.Load(id);
        var cmd = new Escalate(reason);
        ticket.Execute(cmd);
        _ticketRepository.Save(ticket);
        return ExecutionResult.Success();
    }
    catch (ConcurrencyException ex)
    {
        return ExecutionResult.Error(ex);
    }
}
```
