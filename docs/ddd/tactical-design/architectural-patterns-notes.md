# Architectural Patterns Notes

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
Makes it easy for its business logic to become diffused among the different components:  
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
