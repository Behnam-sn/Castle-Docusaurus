---
sidebar_position: 99
---

# Extras

## It’s important to identify the core subdomains whose complexity will affect software design

From a technical perspective,  
It’s important to identify the core subdomains whose complexity will affect software design.  
Because when we are designing the software,  
We have to choose tools and techniques that accommodate the complexity of the business requirements.

## Business Problems

In that case, they won’t be able to completely understand the business logic or why it operates the way it does, which will limit their ability to model and implement an effective solution.

Again, DDD provides guidance and patterns for organizing these domains and avoiding further complexity.  
Tactical design continues the partnership with the domain experts who will recognize their domain language even as they look at the code built by the software teams.

Domain-driven design’s tactical tools address a different aspect of communication issues.

## domain experts

DDD reminds us that software developers are not the only
people involved in building software.
The domain experts, for whom the software is
being built, bring critical understanding of the problems being solved. We create a
partnership throughout the stages of creation as we first apply “strategic design” to
understand the business problem, a.k.a. the domain, and break the problem down
into smaller, solvable, interconnected problems. The partnership with the domain
experts also drives us to communicate in the language of the domain, rather than
forcing those on the business side to learn the technical language of software.

The second stage of a DDD-based project is “tactical design,” where we transform the
discoveries of strategic design into software architecture and implementation. Again,
DDD provides guidance and patterns for organizing these domains and avoiding fur‐
ther complexity. Tactical design continues the partnership with the domain experts
who will recognize their domain language even as they look at the code built by the
software teams.

## crucial for a successful software project

Effective communication and knowledge sharing are crucial for a successful software project.  
Software engineers have to understand the business domain in order to design and build a software solution.

### BC & MOD

Not only does the bounded context pattern protect the consistency of a ubiquitous
language, it also enables modeling. You cannot build a model without specifying its
purpose—its boundary. The boundary divides the responsibility of languages. A lan‐
guage in one bounded context can model the business domain to solve a particular
problem. Another bounded context can represent the same business entities but
model them to solve a different problem.

## business problem

A business problem can be challenges associated with optimizing workflows and processes, minimizing manual labor, managing resources, supporting decisions, managing data, and so on.

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
