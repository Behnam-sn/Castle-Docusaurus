---
sidebar_position: 7
---

# Contract

## What is a Contract?

Models in different bounded contexts can be evolved and implemented independently.  
That said, bounded contexts themselves are not independent.

A system cannot be built out of independent components.  
The components have to interact with one another to achieve the system’s overarching goals.

Implementations in bounded contexts can evolve independently,  
But they have to integrate with one another.

As a result, there will always be touch-points between bounded contexts.  
These are called **contracts**.

## Why Do We Need Contracts?

The need for contracts results from differences in bounded contexts’ models and languages.

Since each contract affects more than one party, they need to be defined and coordinated.

Also, by definition, two bounded contexts are using different ubiquitous languages.  
Which language will be used for integration purposes?

These integration concerns should be evaluated and addressed by the solution’s design.

## What are Bounded Contexts Integration Patterns in DDD?

Domain-driven design has multiple patterns for defining relationships and integrations between bounded contexts.

These patterns are driven by the nature of collaboration between teams working on bounded contexts.

We will divide the patterns into 3 groups, each representing a type of team collaboration:

- Co-Operation
- Customer & Supplier
- Separate Ways

## References

- Learning Domain-Driven Design - Vladik Khononov - O'Reilly
