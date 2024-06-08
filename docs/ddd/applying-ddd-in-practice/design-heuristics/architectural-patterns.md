---
sidebar_position: 3
---

# Architectural Patterns

In Chapter 8, you learned about the three architectural patterns:  
layered architecture, ports & adapters, and CQRS.

Knowing the intended business logic implementation pattern makes choosing an architectural pattern straightforward:

- The event-sourced domain model requires CQRS.  
  Otherwise, the system will be extremely limited in its data querying options, fetching a single instance by its ID only.

- The domain model requires the ports & adapters architecture.  
  Otherwise, the layered architecture makes it hard to make aggregates and value objects ignorant of persistence.

- The Active record pattern is best accompanied by a layered architecture with the additional application (service) layer.  
  This is for the logic controlling the active records.

- The transaction script pattern can be implemented with a minimal layered architecture, consisting of only three layers.

The only exception to the preceding heuristics is the CQRS pattern.

CQRS can be beneficial not only for the event-sourced domain model,  
But also for any other pattern if the subdomain requires representing its data in multiple persistent models.

## References

- Learning Domain-Driven Design - Vladik Khononov - O'Reilly
