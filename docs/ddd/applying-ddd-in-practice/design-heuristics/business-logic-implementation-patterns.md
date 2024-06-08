---
sidebar_position: 2
---

# Business Logic Implementation Patterns

In Chapters 5–7, where we discussed business logic in detail,  
You learned four different ways to model business logic:  
The transaction script, active record, domain model and event-sourced domain model patterns.

Both the transaction script and active record patterns are better suited for subdomains with simple business logic:  
Supporting subdomains or integrating a third-party solution for a generic subdomain, for example.

The difference between the two patterns is the complexity of the data structures.

The transaction script pattern can be used for simple data structures,  
While the active record pattern helps to encapsulate the mapping of complex data structures to the underlying database.

The domain model and its variant, the event-sourced domain model,  
Lend themselves to subdomains that have complex business logic:
Core subdomains.

Core subdomains that deal with monetary transactions,  
Are obligated by law to provide an audit log,  
Or require deep analytics of the system’s behavior are better addressed by the event-sourced domain model.

With all of this in mind,  
An effective heuristic for choosing the appropriate business logic implementation pattern is to ask the following questions:

- Does the subdomain track money or other monetary transactions?  
  Or have to provide a consistent audit log?  
  Or is deep analysis of its behavior required by the business?  
  If so, use the event-sourced domain model. Otherwise...

- Is the subdomain’s business logic complex?  
  If so, implement a domain model. Otherwise...

- Does the subdomain include complex data structures?  
  If so, use the active record pattern. Otherwise...

- Implement a transaction script.

We can use another heuristic to define the difference between complex and simple business logic.  
The line between these two types of business logic is not terribly sharp, but it’s useful.

In general, complex business logic includes complicated business rules, invariants, and algorithms.  
A simple approach mainly revolves around validating the inputs.

Another heuristic for evaluating complexity concerns the complexity of the ubiquitous language itself.
Is it mainly describing CRUD operations,  
Or is it describing more complicated business processes and rules?

Deciding on the business logic implementation pattern according to the complexity of the business logic and its data structures is a way to validate your assumptions about the subdomain type.

Suppose you consider it to be a core subdomain, but the
best pattern is active record or transaction script. Or suppose what you believe is a
supporting subdomain requires a domain model or an event-sourced domain model;
in this case, it’s an excellent opportunity to revisit your assumptions about the subdo‐
main and business domain in general. Remember, a core subdomain’s competitive
advantage is not necessarily technical.

## References

- Learning Domain-Driven Design - Vladik Khononov - O'Reilly
