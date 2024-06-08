---
sidebar_position: 3
---

# Communication Patterns

## What are Communication Patterns?

Up this point you learn about,  
Tactical design patterns that define the different ways to implement a system’s components:

- How to model the business logic
- And how to organize the internals of a bounded context architecturally

In this chapter,  
We will step beyond the boundaries of a single component,  
And discuss the patterns for organizing the flow of communication across a system’s elements.

The patterns you will learn about in this chapter facilitate cross-bounded context communication,  
Address the limitations imposed by aggregate design principles,  
And orchestrate business processes spanning multiple system components.

## Conclusion

In this chapter, you learned the different patterns for integrating a system’s components.

The chapter began by exploring patterns for model translations that can be used to implement anticorruption layers or open-host services.

We saw that translations can be handled on the fly or can follow a more complex logic, requiring state tracking.

The outbox pattern is a reliable way to publish aggregates’ domain events.
It ensures that domain events are always going to be published, even in the face of different process failures.

The saga pattern can be used to implement simple cross-component business pro‐
cesses. More complex business processes can be implemented using the process man‐
ager pattern. Both patterns rely on asynchronous reactions to domain events and the
issuing of commands.

## References

- Learning Domain-Driven Design - Vladik Khononov - O'Reilly
