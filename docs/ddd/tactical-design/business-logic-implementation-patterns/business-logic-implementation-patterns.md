---
sidebar_position: 1
---

# Business Logic Implementation Patterns

## What Problem Business Logic Implementation Patterns is Trying to Solve?

Business logic is the most important part of software.  
It’s the reason the software is being implemented in the first place.

As we saw in strategic design,  
Not all business subdomains are created equal.

Different subdomains have different levels of strategic importance and complexity.

DDD’s tactical patterns,  
Allow us to write code in a way that,  
Reflects the business domain,  
Addresses its goals,  
And speaks the ubiquitous language of its bounded context.

## What are Business Logic Implementation Patterns?

Different ways to model and implement business logic code:

- ### Transaction Script Pattern

  This pattern organizes the system’s operations as simple, straightforward procedural scripts.

  The procedures ensure that each operation is transactional (either it succeeds or it fails).

  The transaction script pattern lends itself to supporting subdomains,  
  With business logic resembling simple, ETL-like operations.

- ### Active Record Pattern

  When the business logic is simple but operates on complicated data structures,  
  You can implement those data structures as active records.

  An active record object is a data structure that provides simple CRUD data access methods.

- ### Domain Model Pattern

  Domain Model Pattern is the DDD's way of implementing complex business logic.

  The domain model’s building blocks tackle the complexity of the business logic,  
  By encapsulating it in the boundaries of value objects and aggregates.

- ### Event-Sourced Domain Model Pattern

  Expand the domain model pattern by modeling the dimension of time.

## References

- Learning Domain-Driven Design - Vladik Khononov - O'Reilly
