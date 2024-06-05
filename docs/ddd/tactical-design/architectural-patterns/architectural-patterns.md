---
sidebar_position: 7
---

# Architectural Patterns

The tactical patterns discussed up to this point in the book defined the different ways to model and implement business logic.

In this chapter, we will explore tactical design decisions in a broader context:  
The different ways to orchestrate the interactions and dependencies between a system’s components.

## Business Logic Versus Architectural Patterns

Business logic is the most important part of software system;  
However, it is not the only part of a software system.

To implement functional and nonfunctional requirements,  
The codebase has to fulfill more responsibilities.

It has to interact with users to gather input and provide output,  
And it has to use different storage mechanisms to persist state,  
And integrate with external systems and information providers.

The variety of concerns that a codebase has to take care of,  
Makes it easy for its business logic,  
To become diffused among the different components.

That is, for some of the logic to be implemented in the user interface or database,  
Or be duplicated in different components.

Lacking strict organization in implementation concerns makes the codebase hard to change.

When the business logic has to change,  
It may not be evident what parts of the codebase have to be affected by the change.

The change may have unexpected effects on seemingly unrelated parts of the system.

Conversely, it may be easy to miss code that has to be modified.

All of these issues dramatically increase the cost of maintaining the codebase.

Architectural patterns introduce organizational principles for the different aspects of a codebase,  
And present clear boundaries between them:  
How the business logic is wired to the system’s input, output, and other infrastructural components.

This affects how these components interact with each other:  
What knowledge they share and how the components reference each other.

Choosing the appropriate way to organize the codebase,  
Or the correct architectural pattern,  
Is crucial to support implementation of the business logic in the short term,  
And alleviate maintenance in the long term.

Let’s explore 3 predominant application architecture patterns and their use cases:

- Layered Architecture
- Ports & Adapters
- CQRS

## Scope

The patterns we’ve discussed—layered architecture, ports & adapters architecture, and CQRS—should not be treated as system-wide organizational principles. These are not necessarily high-level architecture patterns for a whole bounded context either.

Consider a bounded context encompassing multiple subdomains.  
The subdomains can be of different types: core, supporting, or generic.

Even subdomains of the same type may require different business logic and architectural patterns.
Enforcing a single, bounded, context wide architecture will inadvertently lead to accidental complexity.

Our goal is to drive design decisions according to the actual needs and business strategy.  
In addition to the layers that partition the system horizontally,  
We can introduce additional vertical partitioning.

It’s crucial to define logical boundaries for modules encapsulating distinct business subdomains and use the appropriate tools for each.

Appropriate vertical boundaries make a monolithic bounded context a modular one and help to prevent it from becoming a big ball of mud.

As we will discuss in Chapter 11, these logical boundaries can be refactored later into physical boundaries of finer-grained bounded contexts.

## Conclusion

The layered architecture decomposes the codebase based on its technological concerns.  
Since this pattern couples business logic with data access implementation,  
It’s a good fit for active record–based systems.

The ports & adapters architecture inverts the relationships:  
It puts the business logic at the center and decouples it from all infrastructural dependencies.  
This pattern is a good fit for business logic implemented with the domain model pattern.

The CQRS pattern represents the same data in multiple models.  
Although this pattern is obligatory for systems based on the event-sourced domain model,  
it can also be used in any systems that need a way of working with multiple persistent models.

The patterns we will discuss in the next chapter address architectural concerns from a
different perspective: how to implement reliable interaction between different com‐
ponents of a system.
