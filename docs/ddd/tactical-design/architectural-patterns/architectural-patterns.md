---
sidebar_position: 2
---

# Architectural Patterns

## What are Architectural Patterns?

The tactical patterns discussed up to this point,  
Defined the different ways to model and implement business logic.

In this chapter, we will explore tactical design decisions in a broader context:  
The different ways to orchestrate the interactions and dependencies between a system’s components.

<!-- ## Business Logic Versus Architectural Patterns -->

## What Problem Architectural Patterns are Trying to Solve?

### Misplacing Business Logic

Business logic is the most important part of software system;  
However, it is not the only part of a software system.

To implement functional and nonfunctional requirements,  
The codebase has to fulfill more responsibilities:

- It has to interact with users to gather input and provide output
- It has to use different storage mechanisms to persist state
- It has to integrate with external systems and information providers

The variety of concerns,  
That a codebase has to take care of,  
Makes it easy for its business logic,  
To become diffused among the different components.

That may result in some of the logic to be implemented in the user interface or database, or be duplicated in different components.

### Handling Change

Lacking strict organization in implementation concerns makes the codebase hard to change.

When the business logic has to change,  
It may not be evident what parts of the codebase have to be affected by the change.

The change may have unexpected effects on seemingly unrelated parts of the system.  
Conversely, it may be easy to miss code that has to be modified.

All of these issues dramatically increase the cost of maintaining the codebase.

## What is Architectural Patterns Solution?

Architectural patterns introduces,  
Organizational principles for the different aspects of a codebase,  
And present clear boundaries between them.

<!-- How the business logic is wired to the system’s input, output, and other infrastructural components. -->

This affects how components interact with each other:  
What knowledge they share,  
And how the components reference each other.

Choosing the appropriate way to organize the codebase or the correct architectural pattern,  
Is crucial to support implementation of the business logic in the short term,  
And alleviate maintenance in the long term.

Let’s explore 3 predominant application architecture patterns and their use cases:

- ### Layered Architecture

  The layered architecture decomposes the codebase based on its technological concerns.  
  Since this pattern couples business logic with data access implementation,  
  It’s a good fit for active record based systems.

- ### Ports & Adapters

  The ports & adapters architecture inverts the relationships:  
  It puts the business logic at the center and decouples it from all infrastructural dependencies.  
  This pattern is a good fit for business logic implemented with the domain model pattern.

- ### CQRS

  The CQRS pattern represents the same data in multiple models.  
  Although this pattern is obligatory for systems based on the event-sourced domain model,  
  It can also be used in any systems that need a way of working with multiple persistent models.

## How to Use Architectural Patterns?

The layered architecture, ports & adapters and CQRS patterns,  
Should not be treated as system-wide organizational principles.

These are not necessarily high-level architecture patterns for a whole bounded context either.

Consider a bounded context encompassing multiple subdomains.  
The subdomains can be of different types: core, supporting, or generic.

Even subdomains of the same type may require different business logic and architectural patterns.  
Enforcing a single, bounded context wide architecture will inadvertently lead to accidental complexity.

Our goal is to drive design decisions according to the actual needs and business strategy.  
In addition to the layers that partition the system horizontally,  
We can introduce additional vertical partitioning.

It’s crucial to define logical boundaries for modules encapsulating distinct business subdomains and use the appropriate tools for each.

Appropriate vertical boundaries make a monolithic bounded context a modular one and help to prevent it from becoming a big ball of mud.

## References

- Learning Domain-Driven Design - Vladik Khononov - O'Reilly
